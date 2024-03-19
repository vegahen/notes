installed_packages=$(brew list --formula | sed "s/^/ /; s/$/$/")

for package in $(brew leaves)

brew deps --tree --formula $package | grep -E "$installed_packages|^$package$|^$"
