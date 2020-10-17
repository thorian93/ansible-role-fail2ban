# Ansible Role: Fail2Ban

This role manages fail2ban on Debian/Ubuntu, RHEL/CentOS and Fedora servers.

[![Ansible Role: Fail2Ban](https://img.shields.io/ansible/role/51322?style=flat-square)](https://galaxy.ansible.com/thorian93/ansible_role_fail2ban)
[![Ansible Role: Fail2Ban](https://img.shields.io/ansible/quality/51322?style=flat-square)](https://galaxy.ansible.com/thorian93/ansible_role_fail2ban)
[![Ansible Role: Fail2Ban](https://img.shields.io/ansible/role/d/51322?style=flat-square)](https://galaxy.ansible.com/thorian93/ansible_role_fail2ban)

## Here be Dragons!

If you misconfigure Fail2Ban, you will lose network based access to your server! Depending on the settings for a long time!
Furthermore this role enables some jails by default depending on what services are detected on the server. See `templates/jail.local.j2` for more details.

## Known issues

None.

## Requirements

No special requirements; note that this role requires root access, so either run it in a playbook with a global `become: yes`, or invoke the role in your playbook like:

    - hosts: foobar
      roles:
        - role: ansible-role-fail2ban
          become: yes

## Role Variables

    fail2ban_ignoreip: 127.0.0.1/8

Set a list of IPs ignored by Fail2Ban.

    fail2ban_bantime: 432000  # 5 days

Set the time in seconds an IP is locked out.

    fail2ban_findtime: 86400  # 1 day

Set the time in seconds Fail2Ban will look into the past to find failed logins.

    fail2ban_maxretry: 3

Set how many failed logins have to occur before Fail2Ban locks an IP out.

    fail2ban_alert_mail: root@localhost

Set an email address to which Fail2Ban can send alerts.

    fail2ban_loglevel: INFO
    fail2ban_logtarget: /var/log/fail2ban.log
    fail2ban_syslog_target: /var/log/fail2ban.log
    fail2ban_syslog_facility: 1

Configure the logging of Fail2Ban.

    fail2ban_monitoring_cmk: 'false'

If you use Checkmk as a monitoring solution you can enable the corresponding check plugin here.

    fail2ban_services_custom: []

Configure custom jails you want to use. See `defaults/main.yml` for more details on this.

## Dependencies

[![Ansible Role: Webserver](https://img.shields.io/ansible/role/51301?style=flat-square)](https://galaxy.ansible.com/thorian93/ansible_role_webserver)</br>
*For webserver detection.*

## OS Compatibility

This role ensures that it is not used against unsupported or untested operating systems by checking, if the right distribution name and major version number are present in a dedicated variable named like `<role-name>_stable_os`. You can find the variable in the role's default variable file at `defaults/main.yml`:

    role_stable_os:
      - Debian 10
      - Ubuntu 18
      - CentOS 7
      - Fedora 30

If the combination of distribution and major version number do not match the target system, the role will fail. To allow the role to work add the distribution name and major version name to that variable and you are good to go. But please test the new combination first!

Kudos to [HarryHarcourt](https://github.com/HarryHarcourt) for this idea!

## Example Playbook

    ---
    - name: "Run role."
      hosts: all
      become: yes
      roles:
        - ansible-role-fail2ban

## Acknowledgements

This role is based on the work by [resmo](https://github.com/resmo): [Ansible Fail2Ban Role](https://github.com/resmo/ansible-role-fail2ban). Kudos to him for his work!

## Contributing

Please feel free to open issues if you find any bugs, problems or if you see room for improvement. Also feel free to contact me anytime if you want to ask or discuss something.

## Disclaimer

This role is provided AS IS and I can and will not guarantee that the role works as intended, nor can I be accountable for any damage or misconfiguration done by this role. Study the role thoroughly before using it.

## License

MIT

## Author Information

This role was created in 2020 by [Thorian93](http://thorian93.de/).
