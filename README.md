# mruby-linux-namespace   [![Build Status](https://travis-ci.org/haconiwa/mruby-linux-namespace.svg?branch=master)](https://travis-ci.org/haconiwa/mruby-linux-namespace)

A mruby gem using unshare/setns to control linux namespce.

## install by mrbgems

- add conf.gem line to `build_config.rb`

```ruby
MRuby::Build.new do |conf|

  # ... (snip) ...

  conf.gem :github => haconiwa/mruby-linux-namespace'
end
```

## example

```ruby
> Namespace.getuid
 => 500
> Namespace.getgid
 => 500

> Namespace.unshare(Namespace::CLONE_NEWUSER|Namespace::CLONE_NEWNET)
 => 0

> Namespace.getuid
 => 65534
> Namespace.getgid
 => 65534

> File.open('/proc/self/uid_map','wb+').write('0 500 1')
 => 7
> File.open('/proc/self/setgroups','w+').write('deny')
 => 4
> File.open('/proc/self/gid_map','wb+').write('0 500 1')
 => 7
>
 => nil
> Namespace.getuid
 => 0
> Namespace.getgid
 => 0
>
```

## License

under the MIT License: see LICENSE file
