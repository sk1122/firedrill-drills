# Contributing a drill

A drill turns one rule your company believes it follows into a check with evidence. Good hub drills are rules many teams share.

## What a drill needs before it is merged

1. **It validates.** `firedrill validate drills` passes, with no warnings.
2. **It has test cases.** A `<slug>.test.yaml` beside the drill, with at least one passing, one failing and one not-applicable case, and `firedrill test drills` passes.
3. **It says who and why.** `author` is your GitHub handle, `fix` tells the reader what to change, and `maps_to` lists the controls it supports, such as `SOC2:CC8.1`.
4. **A maintainer approves the pull request.**

If the drill needs a fact only a newer Firedrill has, add `requires: ">= x.y.z"`. Older versions will refuse to install it and say why.

## Steps

1. Copy `template/example.drill.yaml` and `template/example.test.yaml` to `drills/<pack>/<slug>.drill.yaml` and `drills/<pack>/<slug>.test.yaml`. The drill's `id` must be `<pack>/<slug>`, matching its path. Use an existing pack when one fits.
2. Write the drill. `firedrill validate` lists the facts and fields it may read.
3. Write the test cases. Each case gives the value of every fact the drill fetches, by its alias, and the verdict it must give. For a drill with `for_each`, give the `target` too.
4. Run the checks:

   ```bash
   firedrill validate drills
   ```

   ```bash
   firedrill test drills
   ```

   ```bash
   firedrill hub index . --out index.json
   ```

5. Commit with a sign-off (`git commit -s`) and open a pull request.

## What will not be merged

- Drills that write to, or try to change, any system. Firedrill only reads.
- Drills whose evidence would hold secrets or personal data beyond what the facts already return.
- Drills that only restate another drill with a different threshold. Teams can edit thresholds in their own copy.
