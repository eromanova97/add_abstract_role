# add_abstract_role
The bash script to add the `[role="_abstract"]` tag to modules and assemblies.

After its deprecation, the `[role="_abstract"]` tag is now required again because the DITA automation needs it to correctly recognize the document’s introduction.

>***NOTE***: **This script was created with the help of Claude Code tool.

## Steps
1. Download the script and put it to the folder with your `.adoc` files, where you want the script to run, for example to the `modules/` folder.
2. Make it executable (`chmod +x add_abstract_role.sh`).
3. Run the script: `./add_abstract_role.sh`

## How it works
- **For modules**, it will work for those files that have concept, reference, or procedure type correctly assigned:
    - It will add the `[role="_abstract"]` tag after the level zero heading, after one blank line.
- **For assemblies**, it will work if you have the `:_mod-docs-content-type: ASSEMBLY` type correctly assigned:
    - It will add the `[role="_abstract"]` tag after `toc::[]`, after one blank line.

>*NOTE*: 
>
>If you do not have blank lines after your zero level headings in modules and after toc::[] in assemblies, the script will add the blank line together with the abstract tag.
>
>The script will also not update any assembly files that lack `toc::[]`. Instead, you will get a `Warning` message:
>```
>⚠ Warning: Assembly file <your-file>.adoc does not contain 'toc::[]' line - skipping
>```

## Tweaking:
The file currenlty executes on all `*.adoc` files. If you are in the main repo and need some filtering, simply change the following line:
```
find . -name "*.adoc" -type f | while read -r file; do
```
-> change the `-name "*.adoc"` part to whatever you need, for example, if you want files that start with the `monitoring-*` prefix, simply change it to: `-name "monitoring-*.adoc"`:
```
find . -name "monitoring-*.adoc" -type f | while read -r file; do
```
