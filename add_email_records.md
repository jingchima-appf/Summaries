## Write test files
- To test this controller, may need to first create a csv file, and then send the file to controller.\
So first need to upload the file, and then send it.
### Problems:
- Whne use `script/start` to start server, request.body is of type `PhusionPassenger::Utils::TeeInput`. But when using unit test, it becomes `StringIO`.
- Not able to upload and send file correcly. 
  
Tried this method `fixture_file_upload('files/test.csv','text/csv')`, but content 
received by controller is incorrect. \
Specifically, in test.csv file, contents are :
```
email_address,status,sub_status
test@example.com,invalid,mailbox_not_found
```
Use the following code to send to controller
```ruby 
    test_file = fixture_file_upload '/files/test.csv', 'text/csv'
    post emails_insert_path, headers: @auth_headers,
         params: {body: test_file}
```
In controller, if we test the file received like this:
```ruby
   file = request.body
   puts file.gets
```
Got this result: `------------XnJLe9ZIbbGUYtzPQJ16u1`


## Batch Email Validation
- Currently Zerobounce has no API for bulk email validation. \
So if we want to create api for batch email validation, we have to do email validation for each single email_address. This is 
essentially the same as <b>for each eamil, send to our own email validatation route<b>
  
- What is given as input? A file, or an array as param in get request?
