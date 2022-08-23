busted
======

[![Luacheck Lint Status](https://img.shields.io/github/workflow/status/lunarmodules/busted/Luacheck?label=Luacheck&logo=Lua)](https://github.com/lunarmodules/busted/actions?workflow=Luacheck)
[![Busted Test Status](https://img.shields.io/github/workflow/status/lunarmodules/busted/Busted?label=Linux%20Build&logo=Github)](https://github.com/lunarmodules/busted/actions?workflow=Busted)
[![Join the chat at https://gitter.im/lunarmodules/busted](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/lunarmodules/busted?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)



busted is a unit testing framework with a focus on being **easy to
use**. Supports Lua >= 5.1, luajit >= 2.0.0, and moonscript.

Check out the [official docs](https://lunarmodules.github.io/busted/) for
extended info.

busted test specs read naturally without being too verbose. You can even
chain asserts and negations, such as `assert.is_not.equal`. Nest blocks of
tests with contextual descriptions using `describe`, and add tags to
blocks so you can run arbitrary groups of tests.

An extensible assert library allows you to extend and craft your own
assert functions specific to your case with method chaining. A modular
output library lets you add on your own output format, along with the
default pretty and plain terminal output, JSON with and without
streaming, and TAP-compatible output that allows you to run busted specs
within most CI servers.

```lua
describe('Busted unit testing framework', function()
  describe('should be awesome', function()
    it('should be easy to use', function()
      assert.truthy('Yup.')
    end)

    it('should have lots of features', function()
      -- deep check comparisons!
      assert.same({ table = 'great'}, { table = 'great' })

      -- or check by reference!
      assert.is_not.equals({ table = 'great'}, { table = 'great'})

      assert.falsy(nil)
      assert.error(function() error('Wat') end)
    end)

    it('should provide some shortcuts to common functions', function()
      assert.unique({{ thing = 1 }, { thing = 2 }, { thing = 3 }})
    end)

    it('should have mocks and spies for functional tests', function()
      local thing = require('thing_module')
      spy.spy_on(thing, 'greet')
      thing.greet('Hi!')

      assert.spy(thing.greet).was.called()
      assert.spy(thing.greet).was.called_with('Hi!')
    end)
  end)
end)
```

Contributing
------------

See [CONTRIBUTING.md](https://github.com/lunarmodules/busted/blob/master/CONTRIBUTING.md).
All issues, suggestions, and most importantly pull requests are welcome.

Testing
-------

You'll need `libev` to run async tests. Then do the following, assuming you
have luarocks installed:

Install these dependencies for core testing:

```
luarocks install copas
luarocks install lua-ev scm --server=http://luarocks.org/repositories/rocks-scm/
luarocks install moonscript
```

(Note: you must have `libev` installed to run `lua-ev`; you can `brew install libev` or `apt-get install libev-dev`)

Then to reinstall and run tests:

```
luarocks remove busted --force
luarocks make
busted spec
```

License
-------

Copyright 2012-2020 Olivine Labs, LLC.
MIT licensed. See [LICENSE for details](https://github.com/lunarmodules/busted/blob/master/LICENSE).
