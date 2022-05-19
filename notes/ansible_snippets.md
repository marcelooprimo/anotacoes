##**Coleta as informações sobre uma lista de pacotes e imprime a saída**
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

##**Imprime mensagem e a variável registrada**
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

##**Imprime mensagem e a variável registrada**
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

