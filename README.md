# CScan: Scan Your CFI's Failed Protections

This is the CScan part of source code of our CCS'20 paper "Finding Cracks in
Shields: On the Security of Control Flow Integrity Mechanisms".

Supported modes (see `main.rs`). See branch `legacy-release` for more CFIs.

```rust
    let verifier: Box<dyn CfiVerifier> = match opt.mode.as_str() {
        "cfi-lb" => Box::new(verifier::CfiLbVerifier::new(&mut dbg)),
        "mcfi" => Box::new(verifier::MCfiVerifier::new(&mut dbg)),
        "llvm" => Box::new(verifier::LlvmVerifier::new(&mut dbg)),
        _ => panic!("unsupported CFI system ({:?})", opt.mode),
    };
```

To support a new CFI, add your verifier in `src/verifier.rs`.


When using CScan for a publication, please cite our work:

```
@inproceedings{DBLP:conf/ccs/LiWZCYL20,
  author    = {Yuan Li and
               Mingzhe Wang and
               Chao Zhang and
               Xingman Chen and
               Songtao Yang and
               Ying Liu},
  editor    = {Jay Ligatti and
               Xinming Ou and
               Jonathan Katz and
               Giovanni Vigna},
  title     = {Finding Cracks in Shields: On the Security of Control Flow Integrity
               Mechanisms},
  booktitle = {{CCS} '20: 2020 {ACM} {SIGSAC} Conference on Computer and Communications
               Security, Virtual Event, USA, November 9-13, 2020},
  pages     = {1821--1835},
  publisher = {{ACM}},
  year      = {2020},
  url       = {https://doi.org/10.1145/3372297.3417867},
  doi       = {10.1145/3372297.3417867},
  timestamp = {Thu, 05 Nov 2020 10:10:36 +0100},
  biburl    = {https://dblp.org/rec/conf/ccs/LiWZCYL20.bib},
  bibsource = {dblp computer science bibliography, https://dblp.org}
}
```

# How to use?
Users can use the `help` option to view specific usage.

## Example
```
RUST_LOG=info,cfifuzz::tester=trace  ./cfifuzz --export=xxx.json --mode=$model -- ./binary/$model/$command
```

# Note

CScan have two versions respectively in `new-release` and `legacy-release` branches. 
The legacy version of CScan can test all CFI schemes evaluated in the publication, while the new version only updates some of the CFI schemes.
The difference between the new version and the old version is that the new version is easier to expand and has better performance, but does not affect the CFI test results.
We recommend users use the new version for expansions.
If users want to test the CFI mechanisms mentioned in the paper, the legacy version can be used.