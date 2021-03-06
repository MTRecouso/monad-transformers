#Overview 

The package consists of the following components: 

## Object wrapper 

The [object wrapper](wrapper.md), exposed via the `mtl.make` function, combines one or several monad  transformer definitions and mixes them into one  [Fantasy Land compliant](https://github.com/fantasyland/fantasy-land) monad. 

    const mtl = {}
    const createStack = require('./stack')
    mtl.make = function () {
      return createStack(Array.prototype.slice.call(arguments)).constructor
    }
    
## Monad transformer definitions 

The library contains four [monad transformer definitions](api.md), distributed in two packages: `data` and `comp`. It also contains three versions of the identity monad transformer, useful as a reference when implementing [custom monad transformers](implementing-transformer.md). 



    mtl.data = require('./data')
    mtl.comp = require('./comp')
    mtl.id = require('./id')
    
    
## Base monads 

When stacking monad transformers, a you must place one plain monad at the bottom of the stack. This monad serves as the stack's base.  

By default, the package uses the identity monad as a base but it also defines a wrapper which allow you to use the [Task monad from Folktale](https://github.com/folktale/data.task) as a base. 

    
    mtl.base = require('./base')
    
## Predefined stacks 

The library features five predefined monad stacks. 



    mtl.simple = mtl.make(mtl.data.maybe, mtl.data.writer)
    mtl.stateful = mtl.make(mtl.data.maybe, mtl.data.writer, mtl.comp.state)
    mtl.list = mtl.make(mtl.data.list, mtl.data.maybe, mtl.data.writer)
    mtl.statelist = mtl.make(mtl.data.list, mtl.data.maybe, mtl.data.writer, mtl.comp.state)
    
    mtl.advanced = mtl.make(mtl.base.task, mtl.data.maybe, mtl.data.writer, mtl.comp.state)
    


## Helpers 

Some helper functions that we want to keep handy: 

    const helpers = require('./helpers')
    mtl.curry = helpers.curry
    mtl.compose = helpers.compose
    
    module.exports = mtl


[_View in GitHub_](../lib/main.js) 

    
