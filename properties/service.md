## Questions

### Database:
- <s>Which sql database should we use? Mysql, postsql, sqlite?</s> Use mysql
- <s>Should uuid be of string type?</s> yes
- <s>Should we allow update by client-side in the database? It seems the data in database comes from data-stream, if we allow client to change the data, won't there be inconsistency?</s> let's allow it for now
- Should we use id or uuid?

### Controller:
- API: current api is as follows
  - show: for both single and multiple vhosts
    - if uuid is speficied, only return information of that vhosts
    - else if address is specified, return all vhosts with that address
    - else if vhost_endpoint is specified, return all vhosts with that vhost_endpoint
    - else return unprocessible-entity 
  - update: only for single vhost
    - if uuid is speficied(means not blank), update that vhost with new address and end_point. Always return :ok.
    - else return not_found
   
### Configuration Problems
- health_check, authentication check, do we need to implement them?
- Configuration files \
  - root folder 
  
  |properties_app | users_app           | 
  |---------------|--------------------:|
  |               |<s>gemsurance</s>           |
  |               |gitignore            |
  |               | <s>.rubocop.yml</s>        |
  |               | <s>.ruby-version</s>       |
  |               | appspec.yml         |
  |               | secrets_manifest.yml|
  |               |                     |

  - tmp/pid folder
  
  |properties_app | users_app           | 
  |---------------|--------------------:|
  |pit_tty_map.yml|                     |
   
  - config folder
    - envivironment folder
    
     |file |properties_app | users_app           | 
     |---  |:-------------:|--------------------:|
     |development|<s>config.active_record.migration_error = :page_load</s>|   |
     |production|<s>config.log_level = :debug</s>|<s>config.log_level = :info</s>|
     | production   |<s>config.active_record.dump_schema_after_migration = false</s>|  |
  
    - initializers folder
    
     |file |properties_app | users_app           | 
     |---  |:-------------:|--------------------:|
     |    |               | <s>silencer.rb </s>      |
     |     |<s>backtrace silencers</s>|                 |
     |     |<s>application_controller_renderer.rb</s>|  |
   
    - <s>ONLY users_app has `settings` folder</s>
      
    - root folder
    
      |file |properties_app | users_app           | 
      |---  |:-------------:|--------------------:|
      |secrets.yml|         | settings for appfolio|
      | <s>puma.rb</s> | <s>has puma.rb</s>   |                 |
      |<s>application.rb</s>| .    |  <s> appfolio settings</s> | 
      |<s>database.yml| how to configure this file | null|
      
