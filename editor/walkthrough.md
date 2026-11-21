## Resume a batch after a failed command

Returns [next offset, next count, failures, first nonzero exit]. The next count becomes zero once failures exceed the allowance. Invalid arguments and nonfinite results return an empty vector.

1. Open an empty file named `pipit-demo.blyx`.
2. Type `blyx-pipit-demo` and select **Pipit — runnable example**. You can also use **Snippets: Fill File with Snippet**.
3. Choose **Blyx: Run File** from the command palette. Change an argument near the end of `fn main()` to try another input.

Expected output

```text
3
2
1
3
```

[Work through the example in the browser](https://www.blyx-lang.space/play?example=package-pipit)
