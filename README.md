This is a repo which reproduces a bug https://github.com/kazu-yamamoto/ghc-mod/issues/607#issuecomment-146145619

To check that it works do:

```
stack build
```

To reproduce bug:

1. open [ghcmod-bug/src/Main.hs](ghcmod-bug/src/Main.hs), make sure
   ghc-mod works (first, it shows no errors, adding some error will
   highlight it).
2. open [ghcmod-bug-lib/src/Lib.hs](ghcmod-bug-lib/src/Lib.hs), make
   sure ghc-mod in that one works also.
3. uncomment `bar :: Int` block in `Lib.hs` to introduce a new symbol, save
4. uncomment `print bar` in
   [ghcmod-bug/src/Main.hs](ghcmod-bug/src/Main.hs).
5. see an error `not in scope: bar`
6. run `stack build`, see that it builds fine
7. save your [ghcmod-bug/src/Main.hs](ghcmod-bug/src/Main.hs)
   again. Now, instead of an error about bar being not in scope, see
   this in your ghc-mod log:

   ```
   <command line>: cannot satisfy -package-id ghcmod-bug-lib-0.1.0.0-1427badc663e1243812e493975dee1cd
   ```

That's it!

