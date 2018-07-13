## Questions

### Database:
- Which sql database should we use? Mysql, postsql, sqlite?
- Should uuid be of string type?
- Should we allow update by client-side in the database? It seems the data in database comes from data-stream, if we allow client
to change the data, won't there be inconsistency?
- Should we use id or uuid?

### Controller:
- API: current api is as follows
  - show: for both single and multiple vhosts
    - if uuid is speficied, only return information of that vhosts
    - else if address is specified, return all vhosts with that address
    - else if vhost_endpoint is specified, return all vhosts with that vhost_endpoint
    - else return unprocessible-entity 
  - update: only for single vhost
    - if uuid is speficied, update that vhost with new address and end_point
    - else return not_found
   
### Configuration Problems
- It seems we don't AWS for this service (so no need for sync_controller?)
- health_check, authentication check, do we need to implement them?

  
