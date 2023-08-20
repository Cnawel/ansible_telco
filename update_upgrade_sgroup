# Update and Upgrade every server in your Hosts Group
Author: Cnawel
Last Update: 8/23
---
- name: Update and Upgrade All Servers
  hosts: your_host_group  # Replace with the name of your host group from your inventory file
  become: yes  # Run tasks with sudo (root) privileges

  tasks:
    - name: Detect the OS distribution
      command: "{{ 'cat /etc/os-release' }}"
      register: os_info
      changed_when: false  # Ensure this task is considered not changed
      check_mode: no  # Ensure this task doesn't change the system in check mode

    - name: Update and upgrade packages on Debian-based systems
      apt:
        update_cache: yes
        upgrade: yes
        autoremove: yes
        autoclean: yes
      when: "'Debian' in os_info.stdout or 'Kali' in os_info.stdout"

    - name: Update and upgrade packages on Red Hat-based systems
      yum:
        name: '*'
        state: latest
      when: "'Red Hat' in os_info.stdout or 'CentOS' in os_info.stdout"

    - name: Update and upgrade packages on Fedora
      dnf:
        name: '*'
        state: latest
      when: "'Fedora' in os_info.stdout"

    - name: Update and upgrade packages on openSUSE
      zypper:
        name: '*'
        state: latest
      when: "'openSUSE' in os_info.stdout"

    - name: Update and upgrade packages on Arch Linux
      pacman:
        upgrade: yes
      when: "'Arch' in os_info.stdout"

    # Add more tasks for additional distributions as needed.
