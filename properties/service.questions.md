## Config Folders
### root:
- Application.rb
  - What does `DEPLOYMENT_CONFIG_FILE = '/etc/appfolio/local.yml'` do? Configuration for production?
```ruby
  class << self
    # TODO: this block of code is borrowed from af_runtime
    DEPLOYMENT_CONFIG_FILE = '/etc/appfolio/local.yml'

    def deployment_env
      @deployment_env ||= begin
        if Rails.env.production?
          ActiveSupport::StringInquirer.new(deployment_config['environment'])
        else
          ActiveSupport::StringInquirer.new(Rails.env.to_s)
        end
      end
    end

    def deployment_config
      @deployment_config ||= YAML.load_file(DEPLOYMENT_CONFIG_FILE)
    end
  end
```

## YAML files
- Where do we call these yaml files? Why we can embed ruby into it?
