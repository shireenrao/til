# Zip Files

Here is a short snippet on processing zip files in memory. The zip file has text files
or other zip files which only have text files. Instead of printing, one can process it
or write to a file.

```python
import zipfile


with zipfile.ZipFile("somezipfile.zip") as zip_archive:
    for item in zip_archive.filelist:
        if item.filename.endswith(".zip"):
            print(f"Zip file {item.filename}")
            child_zip = zip_archive.open(item.filename)
            with zipfile.ZipFile(child_zip) as child_zip_archive:
                for childfile in child_zip_archive.filelist:
                    print(f"Zip file child {childfile.filename}")
                    for line in child_zip_archive.open(childfile.filename):
                        print(line)                   
        else:
            print(f"Regular File {item.filename}")
            for line in zip_archive.open(item.filename):
               print(line)

```
