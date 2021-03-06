patch-management Cookbook
=========================
Ensures specified packages are installed and patched.

Requirements
------------
### Platform:

* Tested on CentOS 6.5
* Tested on Ubuntu 12.04 LTS
* Should work on a wide variety of other *nix systems

### Cookbook Dependencies:

* ohai (https://supermarket.getchef.com/cookbooks/ohai)

Attributes
==========

packages
--------

Hash of packages and their associated minimum version.

Example:

```ruby
node.default['patch-management']['packages'] = {'httpd' => '2.2.15-39.el6', 'bash' => '4.1.2-29.el6'}
```

Recipes
-------

### patch-management::default

* Audits and remediates over specified packages/versions.

### patch-management::audit

* Installs an OHAI plugin (based on the rackerlabs 'packages' plugin: https://github.com/rackerlabs/ohai-plugins/tree/master/plugins) that will catalog installed packages for evaluation. Provides a node['software'] automatic attribute that lists installed packages and their versions.

* Iterates through the hash specified in node['patch-management']['packages'] and sets a node['patch-management']['patched'] boolean to true if all packages are installed and of the correct version or later, or false if any are not present, or of a version different than the one specified in the attribute hash.


### patch-management::remediate

* Iterates through the hash specified in node['patch-management']['packages'] and ensures that the packages contained theirein are installed and at least the version specified in the hash. Installs packages that aren't present, upgrades those that are below the specified version. Will set node['patch-management']['patched'] to true if it completes without issue.

Usage
-----
#### patch-management::default

Include `patch-management` in your node's `run_list`, and be sure to set the "packages" hash for your node/role/etc.

Example:

```json
{
  "patch-management": {
    "packages": {
      "httpd": "2.2.15-39.el6",
      "bash": "4.1.2-29.el6"
    }
  }
}
```

License and Author
------------------

Author:: Chef Software, Inc (support@getchef.com)  
Author:: Nicolas Rycar (nrycar@getchef.com)  
Author:: Andre Elizondo (andre@getchef.com) 

Copyright:: 2014, Chef Software, Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.


Contributing
------------
1. Fork the repository on Github
2. Create a named feature branch (like `add_component_x`)
3. Write your change
4. Write tests for your change (if applicable)
5. Run the tests, ensuring they all pass
6. Submit a Pull Request using Github
