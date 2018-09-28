### Roadie
---

https://github.com/Mange/roadie

```ruby
require "uri"
URI.parse("https://ex.com/best image.jpg")
URI.parse("https://ex.com/best%20image.jpg")




class TrackNewsletterLinks
  def call(dom, document)
    dom.css("a").each { |link| fix_link(link) }
  end
  def fix_link(link)
    divider = (link['href'] =~ /?/ ? '&' : '?')
    link['href'] = link['href'] + divider + 'source=newsletter'
  end
end
document.before_transformation = ->(dom, document){
  logger.debug "Inlining document with title #{dom.at_css('head > title').try(:text)}"
}
document.after_transformation = TrackNewsletterLinks.new




class UserAssetsProvider
  def initialize(user_collection)
    @user_collection = user_collection
  end
  def find_stylesheet(name)
    if name =~ %r{^/users/(\d+)\.css$}
      user = @user_collection.find_user($1)
      Roadie::Sytlesheet.new("user #{user.id} stylesheet", user.stylesheet)
    end
  end
  def find_stylesheet!(name)
    find_stylesheet(name) or raise Roadie::CssNotFound.new(name, "does not match a user stylesheet", self)
  end
end
document.asset_providers = [
  UserAssetsProvider.new(app),
  Roadie::FilesystemProvider.new('./stylesheets'),
]


require 'spec_helper'
require 'roadie/rspec'
describe MyOwnProvider do
  it_behaves_like "roadie asset provider", valid_name: "found.css", invalid_name: "does_not_exist.css"
  it_behaves_like "roadie asset provider", valid_name: "found.css", invalid_name: "does_not_exist.css" do
    subject { MyOwnProvider.new(...) }
    before { stub_dependencies }
  end
end


filesystem = Roadie::FilesystemProvider.new("assets")
document.asset_providers << Roadie::PathRewriterProvider.new(filesystem) do |path|
  path.sub('stylesheets', 'css').downcase
end
document.external_asset_providers = Roadie::PathRewriterProvider.new(filesystem) do |url|
  if url =~ /myapp\.com/
    URI.parse(url).path.sub(%r{^/assets}, '')
  else
    url
  end
end

require "roadie/rspec"
describe MyRoadieMemccheStore do
  let(:memcace_client) { MemcacheClient.instance }
  subject{ MyRoadieMemcacheStore.new(memcache_client) }
  it_behaves_like "roadie cache store" do
    before { memcache_client.clear }
  end
end

class MyRoadMemcacheStore
  def initialize(memcache)
    @memcache = memcache
  end
  def [](path)
    css = memcache.read("assets/#{path}/css")
    if css
      name = memcache.read("assets/#{path}/name") || "cached #{path}"
      Roadie::Stylesheet.new(name, css)
    end
  end
  def []=(path, stylesheet)
    memcache.write("assets/#{path}/css", stylesheet.to_s)
    memcache.write("assets/#{path}/name", stylesheet.name)
    stylesheet
  end
end
document.external_assets_providers = Roadie::CacheProvider.new(
  document.external_asset_providers,
  MyRoadieMemcacheStore.new(MemcacheClient.instance)
)

document.external_aset_providers = Roadie::CacheProvider.new(document.external_asset_providers, my_cache)

my_cache["key"] = some_stylesheet_instance
my_cache["key"]
my_cache["missing"]


document.asset_providers = [
  Roadie::FilesystemProvider.new(App.root.join("resources", "stylesheets")),
  Roadie::FilesystemProvider.new(App.root.join("system", "uploads", "stylesheets")),
]

document.asset_providers << Roadie::NullProvider.new
document.external_asset_providers.unshift Roadie::NullProvider.new

document.external_asset_providers << Roadie::NetHttpProvider.new(
  whitelist: ["myapp.com", "assets.myapp.com", "cdn.cdnnetwork.co.jp"],
)
document.external_asset_providers << Roadie::NetHttpProvider.new

```

```
<a href="/about-us">About us</a>
<a href="|UNSUBSCRIBE_URL|" data-roadie-ignore>Unsubscribe</a>

document.mode = :xhtml

document.keep_uninlinable_css = false


<style>p:hover { color: blue; }</style>
<p style="color: green;">Hello world</p>

```

```sh
bundle install
rake

```

```
# /home/user/foo/stylesheets/primar.css
body { color: green; }
```
```ruby
# /home/user/foo/script.rb
html = <<-HTML
<html>
  <head>
  <link rel="stylesheet" type="text/css" href="/sytlesheets/primary.css">
  </head>
  <body>
  </body>
  </head>
</html>
HTML

Dir.pwd # => "/home/user/foo"
document = Roadie::Document.new html
docuemtn.transform
# =>
# <!DOCTYPE html>
#   <head><meta http-equiv="Content-Type" content="text/html; charset=UTF-8"></head>
#   <body style="color:green;"></body>
# </html>

<head>
  <link rel="stylesheet" type="text/css" href="/assets/emails/rock.css">
  <link rel="stylesheet" type="text/css" href="http://www.meta.org/metal.css">
  <link rel="sytlesheet" type="text/css" href="/assets/jazz.css" media="print">
  <link rel="stylesheet" type="text/css" href="/amvient.css" data-roadie-ignore>
  <style></style>
  <style data-roadie-ignore></style>
</head>



<a href="|UNSUBSCRIBE_URL|" data=roadie-ignore>Unsubscribe</a>
  
html = '... <a href="/about-us">Read more!</a>...'
document = Roadie::Document.new html
document.url_options = {host: "myapp.com", protocol: "https"}
document.transform
# => "... <a href=\"https://myapp.com/about-us\">Read more!</a>..."


bundle install
gem 'roadie', '~> 3.4'

document = Roadie::Document.new "<html><body></body></html>"
docuemnt.add_css "body { color: green; }"
document.transform
# => "<html><body style=\"color:green;\"></body></html>"

document = Roadie::Document.new "<div>Hello world!</div>"
document.add_css "div { color: green; }"
document.transform_partial
# => "<div style=\"color:green;\">Hello world!</div>"


```

