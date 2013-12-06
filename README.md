yum-percona Cookbook
============

The yum-percona cookbook takes over management of the default
repositoryids that ship with CentOS systems. It allows attribute
manipulation of base updates extras centosplus contrib.

Requirements
------------
* Chef 11 or higher
* yum cookbook version 3.0.0 or higher

Attributes
----------
The following attributes are set by default

``` ruby
default['yum']['percona']['description'] = 'Percona MySQL and tools repository'
default['yum']['percona']['baseurl'] = "http://repo.percona.com/centos/6/os/$basearch/"
default['yum']['percona']['gpgkey'] = 'http://www.percona.com/downloads/RPM-GPG-KEY-percona'
default['yum']['percona']['gpgcheck'] = true
default['yum']['percona']['enabled'] = true
```

Recipes
-------
* default - Walks through node attributes and feeds a yum_resource
  parameters. The following is an example a resource generated by the
  recipe during compilation.

```ruby
  yum_repository 'percona' do
    baseurl 'http://repo.percona.com/centos/6/os/$basearch/'
    description 'Percona MySQL and tools repository'
    enabled true
    gpgcheck true
    gpgkey 'http://www.percona.com/downloads/RPM-GPG-KEY-percona'
  end
```

Usage Example
-------------
To disable the Percona repository through a Role or Environment definition

```
default_attributes(
  :yum => {
    :percona => {
      :enabled => {
        false
       }
     }
   }
 )
```

To enable the Percona repository with a wrapper cookbook, place
the following in a recipe:

```
node.default['yum']['percona']['enabled'] = true
include_recipe 'yum-percona'
```

More Examples
-------------
Point the base and updates repositories at an internally hosted server.

```
node.default['yum']['percona']['enabled'] = true
node.default['yum']['percona']['mirrorlist'] = nil
node.default['yum']['percona']['baseurl'] = 'https://internal.example.com/centos/6/os/x86_64'
node.default['yum']['percona']['sslverify'] = false

include_recipe 'yum-percona'
```

License & Authors
-----------------
- Author:: Sean OMeara (<someara@opscode.com>)

```text
Copyright:: 2011-2013 Opscode, Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
