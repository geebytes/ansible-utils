## 1. ansible-utils

基于ansible分布式集群各类环境批量安装工具

## 2. 使用说明

### 3. 环境要求

- Centos7
- Python3 默认使用Python3.7

### 4. 初始化ansible

#### 4.1. 免密登录配置

   由于ansible批量操作需要控制端对所有客户端进行免密码登陆操作，所以需要配置ssh key免密登录

   4.1.1. 修改dev_hosts文件，配置各个节点的ip或域名  

   4.1.2. 执行如下操作,安装ansible并分发控制端ssh 公钥到客户机

```shell
./init_ansible_ssh.sh /data/work/platform/source/matrix/platform/source/ansible/dev_hosts <USER> <PASSWORD>
```

#### 4.2. 修改ansible配置

修改ansible工作目录和安装目录，编辑ansible.cfg

##### 4.2.1.  inventory路径配置

```
inventory      = /data/work/platform/source/matrix/platform/source/ansible-utils/hosts
```

##### 4.2.2. ansible插件安装路径

```
action_plugins     = /usr/local/lib/python3.7/site-packages/ansible/plugins/action
callback_plugins   = /usr/local/lib/python3.7/site-packages/ansible/plugins/callback
connection_plugins = /usr/local/lib/python3.7/site-packages/ansible/plugins/connection
lookup_plugins     = /usr/local/lib/python3.7/site-packages/ansible/plugins/lookup
vars_plugins       = /usr/local/lib/python3.7/site-packages/ansible/plugins/vars
filter_plugins     = /usr/local/lib/python3.7/site-packages/ansible/plugins/filter
test_plugins       = /usr/local/lib/python3.7/site-packages/ansible/plugins/test
```

##### 4.2.3.  配置各节点ip及其他变量参数

编辑hosts文件

- [x] 更新develop节点ip配置
- [x] 更新nodes节点ip配置
- [x] 更新各类路径配置

## 5. 执行Playbook

#### 5.1. playbooks说明

| palybook                     | 说明                             | 备注 |
| ---------------------------- | -------------------------------- | ---- |
| 00.Python-installer.yml      | Python批量安装部署，支持离线安装 |      |
| 01.Pyenv-installer.yml       | Pyenv批量安装部署                |      |
| 02.Supervisord-installer.yml | supervisord批量安装部署          |      |

#### 5.2. 执行playbooks

以Python安装部署为例



##### 5.2.1. 修改配置参数

按需修改ansible-utils/roles/python-installer/vars/main.yml各类变量参数

##### 5.2.3. 执行部署脚本

```shell
ansible-playbook 00.Python-installer.yml
```

