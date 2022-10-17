# Go coverage with -coverpkg

This repository demonstrates how the `-coverpkg` option works when you get test coverage of your projects.

This project has two packages, one is pkg1 and the other is pkg2. The pkg1 has enough tests, it's actually 100%. On the other hand, the pkg2 has no tests.

`without_coverpkg.sh` calculates the "total" coverage using `go test` commands without `-coverpkg`. `with_coverpkg.sh` does the same thing with the `-coverpkg` option. The script lists up dependency packages in the project and pass that to the `-coverpkg` option.

# Outputs

```shell
/workspace/go_cover (master) $ ./without_coverpkg.sh 
?       github.com/xNok/go_cover        [no test files]
ok      github.com/xNok/go_cover/pkg1   0.001s  coverage: 100.0% of statements
?       github.com/xNok/go_cover/pkg2   [no test files]
```

We don't have any tests for `pkg2`, but the shown coverage is 100%.


```shell
/workspace/go_cover (master) $ ./with_coverpkg.sh 
?       github.com/xNok/go_cover        [no test files]
ok      github.com/xNok/go_cover/pkg1   0.001s  coverage: 40.7% of statements in ./...
?       github.com/xNok/go_cover/pkg2   [no test files]
```

Now you see the real total coverage.

# Conclusion

It's good to have `-coverpkg` option in the script to calculate the project-wide test coverage. It can revial hidden untested packages.

However, when you want to see if each package has enough unit tests, you don't want to use the `-coverpkg` option, becasue it makes the test comand output "integrated" coverages.
