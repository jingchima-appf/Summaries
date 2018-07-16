I found two ways to store meta-data in SQL database
## Store dynamic data as in JSON column of SQL database
- Pros:
  - Easy to implement
  - Easy to access attributes for single vhost.
- Cons: 
  - Not able to aggregate over attributes in dynamic data \
    (Example: If in the dynamic data field we have a field called `Cost`, then it's not easy to aggregate over `cost` for different vhosts.
    
## Use EAV table and pivot query
Can be implemented as like this:

|vhost_id|attribute|value|
|--------|:-------:|----:|
|vhost_1 | name    | Jin |
|vhost_2 | height  | 100 | 

- Pros:
  - Can aggregate over dynamic attributes by pivot query
- Cons:
  - Single vhost access may be slower as the table grows
  - Update dynamic attributes can be slow when there are many attributes in meta-data
  
If we don't need to aggregate over dynamic attributes, using json column might be a better way.
