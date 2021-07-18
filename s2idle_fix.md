# s2idle fix

### Preparation
> sudo apt install acpica-tools

### Dumping ACPI table

> mkdir ~/acpi/
cd ~/acpi/
acpidump -b

### Put away oeml.dat to prevent issues
> mv oeml.dat oeml.dat.bak

### Decompile the table
> iasl -e *.dat -d dsdt.dat

### Patching the table: dsdt.dsl

Change from

> DefinitionBlock ("", "DSDT", 2, "HPQOEM", "8760    ", 0x00000000)

```
If (Zero)
{
    Name (_S3, Package (0x04)  // _S3_: S3 System State
    {
        0x03,
        0x03,
        Zero,
        Zero
    })
}
```

to

> DefinitionBlock ("", "DSDT", 2, "HPQOEM", "8760    ", 0x00000001)

```
Name (_S3, Package (0x04)  // _S3_: S3 System State
{
    0x03,
    0x03,
    Zero,
    Zero
})
```

### Compiling the table
> iasl -ve -tc dsdt.dsl

### Making CPIO archive
```
mkdir -p kernel/firmware/acpi
cp dsdt.aml kernel/firmware/acpi
find kernel | cpio -H newc --create > acpi_override.cpio
```

### Attach CPIO to initrd.img
```
cp acpi_override.cpio /boot/
cd /boot/
mv initrd.img initrd.img.bak
cat acpi_override.cpio initrd.img.bak > initrd.img
```