
# Rails::API

![API](https://i.imgflip.com/1e6ocg.jpg)
## Rails for API only apps
Quick walk-through of Rail::API

* What Rails::API provides for API-only apps
* How to work with the middleware you want to include
* How to decide which modules to use in your computer


# CONTENTS

* Installing
* Middleware
* Controller Modules



# Installing
### Creating a new application

 # Generate a new Rails::API app
### $rails new [api_name] --api
> NOTE: You can add -d [database] if you don't want to use postgresql
This will do few things for you:

* It will make your applicationcontroller inherit from ActionController::API instead of ActionController::Base. 

  * Configure the generators to skip generating views, helpers and assets when you generate a new resource.


### Changing an existing application
If you want to take and existing application and make it an API one, then follow these steps.

 * In config/application.rb add the following line at the top of the Application class definition:
Config.api_only = true

 * In config/environments/development.rb, set       config.debug_exception_response_format to configure the format used in responses when errors occur in development mode.

To render an HTML page with debugging information, use the value :default.
 ### config.debug_exception_response_format = :default

 To render debugging information preserving the response format, use the value :api.
 ### config.debug_exception_response_format = :api

NOTE: By default, config.debug_exception_response_format is set to :api, when config.api_only is set to true.

  * Finally, inside app/controllers/application_controller.rb, instead of:

    > class ApplicationController < ActionController::Base
    >  end

    > class ApplicationController < ActionController::API
    >  end



# Middleware
An API application comes with the following middlleware by default:


* Rack::Sendfile
* ActionDispatch::Static
* ActionDispatch::Executor
* ActiveSupport::Cache::Strategy::LocalCache::Middleware
* Rack::Runtime
* ActionDispatch::RequestId
* ActionDispatch::RemoteIp
* Rails::Rack::Logger
* ActionDispatch::ShowExceptions
* ActionDispatch::DebugExceptions
* ActionDispatch::Reloader
* ActionDispatch::Callbacks
* ActiveRecord::Migration::CheckPending
* Rack::Head
* Rack::ConditionalGet
* Rack::ETag


YOU CAN GET A LIST OF ALL MIDDLEWARE IN YOUR APPLICATION :
> $rails middleware

Removing Middleware
If you don't want to use a middleware that is included by default in the API-only middleware set, you can remove it with:


> config.middleware.delete ::Rack::Sendfile


## CONTROLLER MODULES

* An API application (using ActionController::API) comes with the following controller modules by default:
* ActionController::UrlFor: Makes url_for and similar helpers available.
* ActionController::Redirecting: Support for redirect_to.
* AbstractController::Rendering and ActionController::ApiRendering: Basic support for rendering.
* ActionController::Renderers::All: Support for render :json and friends.
* ActionController::ConditionalGet: Support for stale?.
* ActionController::BasicImplicitRender: Makes sure to return an empty response, if there isn't an explicit one.
* ActionController::StrongParameters: Support for parameters white-listing in combination with Active Model mass assignment.
* ActionController::ForceSSL: Support for force_ssl.
* ActionController::DataStreaming: Support for send_file and send_data.
* AbstractController::Callbacks: Support for before_action and similar helpers.
* ActionController::Rescue: Support for rescue_from.
* ActionController::Instrumentation: Support for the instrumentation hooks defined by Action Controller (see the instrumentation guide for more information regarding this).
* ActionController::ParamsWrapper: Wraps the parameters hash into a nested hash, so that you don't have to specify root elements sending POST requests for instance.
* ActionController::Head: Support for returning a response with no content, only headers

## ADDING other modules
* All Action Controller modules know about their dependent modules, so you can feel free to include any modules into your controllers, and all dependencies will be included and set up as well.
* Some common modules you might want to add:
* AbstractController::Translation: Support for the l and t localization and translation methods.
Support for basic, digest or token HTTP authentication:
* ActionController::HttpAuthentication::Basic::ControllerMethods,
* ActionController::HttpAuthentication::Digest::ControllerMethods,
* ActionController::HttpAuthentication::Token::ControllerMethods
* ActionView::Layouts: Support for layouts when rendering.
* ActionController::MimeResponds: Support for respond_to.
* ActionController::Cookies: Support for cookies, which includes support for signed and encrypted cookies. This requires the cookies middleware.
* The best place to add a module is in your ApplicationController, but you can also add modules to individual controllers.


## References:

[Rails](https://guides.rubyonrails.org/api_app.html)
