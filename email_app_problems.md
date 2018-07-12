
## Bulk Email Validation API
### Problems: 
- When client send wrongly-formatted query parameter
  -  `emails=unknown@example.com&emails[]=invalid@example.com` (the first parameter is not an array)
  then the server's response is not elegant. It will response 400 bad request, and show the error message. The error occurs in this code block
  ```ruby 
  def bulk_validation_params
    params.permit(:emails => [])
  end
  ```
  And error message is as follows
  ``` javascript
  "status": 400,
  "error": "Bad Request",
  "exception": "#<Rack::QueryParser::ParameterTypeError: expected Array (got String) for param `emails'>",
  ```
### Possible Solutions
- Use `rescue` in this block:
  ```ruby 
  def bulk_validation_params
    params.permit(:emails => [])
  end
  ```
  change it into:
  ```ruby
  def bulk_validation_params
    begin
      params.permit(:emails => [])
    end
  rescue StandardError => e
  Rails.logger.error "emails_not_array"
  end  
  ```
<hr>
  
  ## CSV API
  ### Problem
  - The most recent version is on branch `jmAddRecords`, but this one can't be automatically merged into master because 
  the base node in master is changed. Should I pull master first and then re-implement this API on another branch? 
  
