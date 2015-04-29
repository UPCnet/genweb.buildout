Error 'No blob file' al recatalogar
===================================

Si al recatalogar ens trobem aquest error vol dir que el fitxer a disc al que fa referencia un arxiu o imatge de plone no existeix. Si no el troba, deixa de catalogar i peta. Pot passar que:

- No haguem copiat els blobs, en cas que estem debugant quelcom, i no ens interessin.
- Necessitem saber quin arxiu no troba

En amdos casos, podem aplicar el seguent patch (en local) al paquet Zope.ZODB3, que evitarà que la recatalogació peti, i ens identificarà al log "live" els arxius .blob que no trobi.

.. code-block:: diff

	--- blob.py
	+++ ZODB/blob.py
	@@ -145,8 +145,11 @@
		     if not to_open:
		         to_open = self._p_blob_committed
		         if to_open:
	+                  try:
		             result = self._p_jar._storage.openCommittedBlobFile(
		                 self._p_oid, self._p_serial, self)
	+                  except:
	+                    result = ''
	  
		         else:
		             self._create_uncommitted_file()
	@@ -650,7 +653,8 @@
		 """
		 filename = self.fshelper.getBlobFilename(oid, serial)
		 if not os.path.exists(filename):
	-            raise POSKeyError("No blob file", oid, serial)
	+            print 'No blob file %s' % filename
	+            #raise POSKeyError("No blob file", oid, serial)
		 return filename
	 
	     def openCommittedBlobFile(self, oid, serial, blob=None):

