# ansible-examples
Ansible Caveats
  - AWS region MUST be specify when you want to use ec2_instance_info anible module

Example: 
```
    - hosts: localhost
       connection: local
  tasks:
    - name: Check Instances Region must be supplied for tag filter
      ec2_instance_info:
        region: us-east-1
        filters:
          "tag:Name": MyTargetEc2Instance
        # instance_ids: i-01a1e47b2d10bf392
      register: ec2_info

    - name: displaying output
      debug: msg="{{item.instance_id}}"
      with_items: "{{ec2_info.instances}}"
```
  - Make sure to check install module when installing pkgs. It is different in each linux flavor 
  
  Example:
  
  Ubuntu 
  ```
  tasks:
    - name: Install apcahe
      apt: name=apache2 state=present update_cache=yes
  ```
  AWS linux/Centos 
  ```
  tasks:
    - package:
       name=httpd state=present update_cache=yes
   ```
   
