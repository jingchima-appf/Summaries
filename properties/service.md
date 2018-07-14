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
- health_check, authentication check, do we need to implement them?
- Configuration files \
  - root folder 
  
  |properties_app | users_app           | 
  |---------------|--------------------:|
  |               |gemsurance           |
  |               |gitignore            |
  |               | .rubocop.yml        |
  |               | .ruby-version       |
  |               | appspec.yml         |
  |               | secrets_manifest.yml|
  |               |                     |

  - tmp/pid folder
  
  |properties_app | users_app           | 
  |---------------|--------------------:|
  | server.pid    |passenger.3000.pid.lock|
  
  - log folder 
  
  |properties_app | users_app           | 
  |---------------|--------------------:|
  |               |newrelic_agent.log   |
  |               |passenger.3000.log   |
  
  - lib folder
  
  |properties_app | users_app           | 
  |---------------|--------------------:|
  |               |(things related to dynomoid)|
  
  
  - config folder
    - envivironment folder
    
     |file |properties_app | users_app           | 
     |---  |:-------------:|--------------------:|
     |development|config.active_record.migration_error = :page_load|   |
     |production|config.log_level = :debug|config.log_level = :info|
     | .   |config.active_record.dump_schema_after_migration = false|  |
  
    - initializers folder
    
     |file |properties_app | users_app           | 
     |---  |:-------------:|--------------------:|
     | .   |               | silencer.rb .       |
     | .   | .             | sync_settings.rb .  |
   
    - ONLY users_app has `settings` folder
      
    - root folder
    
      |file |properties_app | users_app           | 
      |---  |:-------------:|--------------------:|
      |secrets.yml|         | settings for appfolio|
      | puma.rb | has puma.rb   |                 |
      |application.rb| .    |   appfolio settings | 
      |database.yml| how to configure this file | null|
      
