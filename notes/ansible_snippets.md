## **Coleta as informações sobre uma lista de pacotes e imprime a saída**
- Coleta a versão do software e agrupa a saída por servidor
```bash
---
- name: checking version of package
  hosts: all
  become: true
  gather_facts: false
  tasks:
    - name: getting version of package
      yum:
        list: "{{ item }}"
      loop:
        - zlib
        - gzip
      register: package
    - debug:
        var: package
```

## **Imprime mensagem e a variável registrada**
- Mesma função que o anterior, porém apenas para 1 pacote e imprimindo 1 mensagem
```bash
---
- name: checking version of package
  hosts: all
  become: true
  tasks:
    - name: getting version of package
      yum:
        list: zlib
      register: package
    - debug:
        msg: "Server = {{ ansible_nodename }} - Package version = {{ package }}"
```

## **Imprime mensagem e a variável registrada**
- Limita a execução ao host que tem servidor no nome
```bash
---
- name: Example from an Ansible Playbook
  hosts: all
  tasks:
    - name: ping
      ansible.builtin.ping:
      when: "'servidor' in inventory_hostname"
```

## **Obtém a versão do kernel e coleta os serviços que estão em execução**

```bash
---
- name: Checking version of package
  hosts: all
  become: true
  gather_facts: true
  vars:
    newline_character: "\n"
    services_running: []
  tasks:
    - name: kernel version
      debug:
        msg: "{{ ansible_nodename }} has kernel version {{ ansible_kernel }}"

    - name: populate service facts
      service_facts:

    - name: populate running services
      set_fact:
        services_running: "{{ services_running + [item] }}"
      when: hostvars[inventory_hostname]['services']['{{item}}']['state'] == "running"
      with_items: "{{ hostvars[inventory_hostname]['services'].keys() }}"

    - debug:
        msg: "running services: {{ services_running }}"
```

## **Faz o levantamento dos serviços que estão em execução e dos que não estão**
```bash
---
- hosts: localhost
  gather_facts: no
  vars:
    newline_character: "\n"
    services_running: []
    services_NOT_running: []
  tasks:
  - name: populate service facts
    service_facts:

  - name: populate running services
    set_fact:
      services_running: "{{ services_running + [item] }}"
    when: hostvars[inventory_hostname]['services']['{{item}}']['state'] == "running"
    with_items: "{{ hostvars[inventory_hostname]['services'].keys() }}"

  - name: populate NOT running services
    set_fact:
      services_NOT_running: "{{ services_NOT_running + [item] }}"
    when: hostvars[inventory_hostname]['services']['{{item}}']['state'] != "running"
    with_items: "{{ hostvars[inventory_hostname]['services'].keys() }}"

  - debug:
      msg: "running services: {{ services_running }}"

  - debug:
      msg: "NOT running services: {{ services_NOT_running }}"
```