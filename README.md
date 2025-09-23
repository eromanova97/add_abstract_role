# add_abstract_role
The bash script to add the `[role="_abstract"]` tag to modules and assemblies.

>*NOTE*: This script was created with the help of Claude AI tool.

## Steps:
1. Download the script and put it to the folder with your `.adoc` files, where you want the script to run, for example to the `modules/` folder.
2. Make it executable (`chmod +x add_abstract_role.sh`).
3. Run the script: `./add_abstract_role.sh`

## How it works:
- **For modules**, it will work for those files that have concept, reference, or procedure type correctly assigned:
    - It will add the `[role="_abstract"]` tag after the level zero heading, after one blank line.
- **For assemblies**, it will work if you have the `:_mod-docs-content-type: ASSEMBLY` type correctly assigned:
    - It will add the `[role="_abstract"]` tag after `toc::[]`, after one blank line.

>*NOTE*: 
>
>If you do not have blank lines there after your zero level headings in modules and after toc::[] in assemblies. The script will add the blank line together with the abstract tag.
>
>The script will also not update any assembly files that lack `toc::[]`. instead, you will get a `Warning` message:
>```
>⚠ Warning: Assembly file <your-file>.adoc does not contain 'toc::[]' line - skipping
>```

## Tweaking:
The file currenlty executes on all `*.adoc` files. If you are in the main repo and need some filtering, simply change the following line:
```
find . -name "*.adoc" -type f | while read -r file; do
```
-> change the `-name "*.adoc"` part to whatever you need, for example, if you want files that start on `monitoring-*`, simply change it to: `-name "monitoring-*.adoc"`:
```
find . -name "monitoring-*.adoc" -type f | while read -r file; do
```
