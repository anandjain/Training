```
vim ~/chef-repo/cookbooks/first_cookbook/attributes/default.rb`
default['first_cookbook']['name'] = "Anand Jain" 

`vim ~/chef-repo/cookbooks/first_cookbook/templates/motd.erb`
<%= node['first_cookbook']['name'] %>

vim ~/chef-repo/cookbooks/first_cookbook/recipes/default.rb
`template '/etc/motd' do
  source 'motd.erb'
  action :create
end`

##############################################################

include_recipe 'mytomcat::install'

##############################################################

vim ~/chef-repo/cookbooks/first_cookbook/attributes/default.rb

default['first_cookbook']['packages'] = [ "git", "tree", "wget"]



vim ~/chef-repo/cookbooks/first_cookbook/recipes/default.rb

packages = node['first_cookbook']['packages']

`apt_update 'update apt repository' do
  action :update
  only_if node['platform'] == 'ubuntu'
end`


`packages.each do |package_name|
  package package_name do
    action :purge
  end
end`
```
