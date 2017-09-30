
## PSSE - What are your power system elements?
   
   Want to know the number and type of elements in your power system study? It's easy. All you require is the PSSE raw file. Let's use the following example file in the PSSE example directory `savnw.raw`.
                
   Paste this little function in your favourite python editior:
   
   ```python
   from itertools import islice
   def read_rawdata(floc,fname):
       n, data = 0, {}
       with open(floc + fname) as f:
           for line in islice(f,3,None):
               if "0 /" in line:
                   key = line.split("END OF")[1].split("BEGIN")[0].replace(",","")
                   key = key.strip()
                   data[key], n = n, 0
               else: n += 1
       return data
   if __name__ == "__main__":
       floc = r"C:\Program Files (x86)\PTI\PSSE33\EXAMPLE\\" 
       fname = "savnw.raw"
       rawdat = read_rawdata(floc,fname)
   ```
  
  Now, print the contents of the <span style="color:red">rawdat</span> variable with the following bit of code:
  
  ```python
  print {key:value for key, value in rawdat.iteritems() if not value==0}
  ```
  
  The output should be as follows:
  
  ```python
  {'BRANCH DATA': 23, 'BUS DATA': 23, 'INTER-AREA TRANSFER DATA': 4, 'AREA DATA': 3, <br/>
   'GENERATOR DATA': 6, 'LOAD DATA': 8, 'MULTI-SECTION LINE DATA': 2, <br/>
   'FIXED SHUNT DATA': 5, 'TRANSFORMER DATA': 44, 'OWNER DATA': 7, 'ZONE DATA': 4}
  ```
 
  That at a glance gives you the number and type of power system elements in the PSSE example file.
  