<img src="assets/logo.png" width="112" height="112" alt="Pipit logo">

# Pipit

Plan the next CLI batch from child exit codes and a failure allowance. This Blyx workflow framework is part of the command-line tools collection.

A batch script can erase an earlier error when the last child exits successfully. Use the whole exit trace to decide whether work should continue. [Python, subprocess exit status](https://docs.python.org/3/library/subprocess.html#subprocess.CompletedProcess.returncode)

## Install and run

Install [Blyx 0.2.1](https://www.blyx-lang.space/download) with a Rust toolchain and host linker for native builds.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-pipit.git
cd blyx-pipit
blyxc native-run example.blyx
blyxc native-run tests.blyx
```

[Run the editable browser example](https://www.blyx-lang.space/play?example=package-pipit) · [Package page](https://www.blyx-lang.space/packages/pipit) · [Handbook](https://doc.blyx-lang.space/guide/pipit)

## Import the module

Run this in the directory containing your application's entry file.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-pipit.git vendor/pipit
```

```blyx
use vendor::pipit::pipit;

fn main() {
    let codes = [0, 3, 0];
    let total = 8.0;
    let batch = 2.0;
    let tolerance = 1.0;
    let result = pipit_continue_batch(codes, total, batch, tolerance);
    if len(result) == 0 { println!("invalid"); return; }
    let mut i = 0;
    while i < len(result) {
        println!(at(result, i));
        i += 1;
    }
}
```

Expected output

```text
3
2
1
3
```

## API

`pipit_continue_batch(codes, total, batch, tolerance)`

Returns [next offset, next count, failures, first nonzero exit]. The next count becomes zero once failures exceed the allowance. Invalid arguments and nonfinite results return an empty vector. Integers carried in numeric vectors use the exact range from −(2^53−1) to 2^53−1.

| Argument | Domain |
| --- | --- |
| codes | Vector of values, each a whole byte in [0,255] |
| total | A nonnegative exact integer |
| batch | A positive exact integer |
| tolerance | A nonnegative exact integer |

## Run the command-line project

Run the example with your own numbers. Vector arguments accept up to 16 comma-separated entries; use `[]` for an empty vector. The imported API accepts longer vectors. Invalid arguments return a nonzero exit status.

```sh
blyxc native-run project.blyx -- "0,3,0" 8 2 1
```

## Libraries

- [ExitPolicy](https://github.com/Rahulchaube1/blyx-exitpolicy/tree/v0.1.0) — Summarize portable process exit codes without losing the first failure.
- [BatchQuota](https://github.com/Rahulchaube1/blyx-batchquota/tree/v0.1.0) — Bound the next batch of an interrupted command.

This release includes identical copies of both library modules so a tagged clone can build offline.

## Verification and contributions

The regression suite in [tests.blyx](tests.blyx) checks the example, boundary cases and invalid inputs. Include a short reproducer and your compiler version in [an issue](https://github.com/Rahulchaube1/blyx-pipit/issues). The source is dual-licensed under [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE). The package artwork uses [Lucide icons](https://lucide.dev/license); see [artwork notices](assets/NOTICE.txt).

## Connect with Rahul Chaube

[Portfolio](https://www.rahulchaube1.com/) · [GitHub](https://github.com/Rahulchaube1) · [LinkedIn](https://www.linkedin.com/in/rahulchaube1) · [Hugging Face](https://huggingface.co/oncody) · [X](https://x.com/RahulChaube_) · [EverestQ](https://www.everestqai.com/) · [Contact](https://www.rahulchaube1.com/contact)

[Blyx website](https://www.blyx-lang.space/) · [BlyxTorch](https://www.blyx-lang.space/packages/blyxtorch) · [Handbook](https://doc.blyx-lang.space/) · [Community](https://www.blyx-lang.space/community)

Support Rahul’s open-source work through [GitHub Sponsors](https://github.com/sponsors/Rahulchaube1) or [Buy Me a Coffee](https://buymeacoffee.com/rahulchaube).
