# cowrie ansible role

This is a simple role to install [cowrie](https://github.com/micheloosterhof/cowrie) on a server. It
has been tested on Debian Jessie, but nothing is really Debian specific. systemd is assumed to be
the init system, so service files get written to `/etc/systemd/system/cowrie.service`, but that
should be easy enough to change for a different init system. If you do that, please submit a pull
request!

# Variables
There are a ton of role variables available, most of them around configuring cowrie. See
[defaults/main.yml](defaults/main.yml) for the full list, here are the highlights:

* `cowrie_hostname` is the hostname cowrie should show to things that try to connect. Defaults to
`srv04`, just like the default cowrie config.
* `cowrie_redirect_port` is a boolean. If set to true, the systemd service will redirect port 22 to
2222 or whatever `cowrie_port` is set to. Note that if you do this make sure to have real SSH moved
to a different port first! It is set to false by default to prevent accidental lockouts.

All of the default cowrie options can be configured by setting `cowrie_<option>`. Non-default
options go in a dict called `cowrie_settings`. The keys of this dict are the headings in
`cowrie.cfg` and the values are other dicts with key/value pairs of settings. For example, by
default, `cowrie_settings` just configures the json output logging module and looks like this:

```yaml
cowrie_settings:
  output_jsonlog:
    logfile: "{{ cowrie_log_path }}/cowrie.json"
```

Resulting in the following entry in cowrie.cfg:

```
[output_jsonlog]
logfile: log/cowrie.json
```
