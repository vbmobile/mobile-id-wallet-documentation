# Document Reader

The Mobile ID Wallet SDK provides comprehensive support for managing identity documents within the
wallet. Developers can retrieve all stored documents or access a specific document by its unique
identifier. Documents can be added to the wallet by capturing them with the device camera and
optionally using RFID for enhanced security. Stored documents can also be deleted when no longer
needed.


## Read

=== "Android"

    ```kotlin
    launch {
        val result = MobileIdWallet.getInstance().readDocument(
            activity = activity,
            input = ReadDocument.Input(
                params = DocumentReaderParameters(
                    rfidRead = true
                )
            )
        )
    
        if (result.isSuccess) {
            val document = result.getOrNull()?.records
            // handle success here
        } else {
            // handle error here
        }
    }
    ```

=== "iOS"

    ```swift
	extension DocumentsManagerSampleUsage {
	    /// Reads a document using the device camera and optionally RFID, parses its information, and stores it in the wallet.
	    func readDocument() {
	        let yourTopViewController: UIViewController = .init()
	        let parameters: ReadDocumentParameters = .init(readRFID: true)
	        Task {
	            do {
	                let result = try await mobileIdWallet.readDocument(.init(
	                    viewController: yourTopViewController,
	                    readDocumentParameters: parameters
	                ))
	                let document = result.document
	                // handle success here
	            } catch {
	                // handle error here
	            }
	        }
	    }
	}
    ```

## Retrieve stored documents

=== "Android"

    ```kotlin
	launch {
        val result = MobileIdWallet.getInstance().getAllDocuments()
    
        if (result.isSuccess) {
            val document = result.getOrNull()?.records
            // handle success here
        } else {
            // handle error here
        }
    }
    ```

=== "iOS"

    ```swift
	extension DocumentsManagerSampleUsage {
	    /// Retrieves all documents currently stored in the wallet.
	    func getAllDocuments() {
	        Task {
	            do {
	                let result = try await mobileIdWallet.getAllDocuments()
	                let records = result.records
	                // handle success here
	            } catch {
	                // handle error here
	            }
	        }
	    }
	}
    ```

## Get Document

=== "Android"

    ```kotlin
	launch {
        val result = MobileIdWallet.getInstance().getDocument(
            GetDocument.Input(documentId)
        )
    
        if (result.isSuccess) {
            val document = result.getOrNull()?.record
            // handle success here
        } else {
            // handle error here
        }
    }
    ```

=== "iOS"

    ```swift
	extension DocumentsManagerSampleUsage {
	    /// Retrieves a specific document from the wallet using its unique identifier.
	    func getDocumentById() {
	        Task {
	            do {
	                let documentId = "<YOUR_DOCUMENT_ID>"
	                let result = try await mobileIdWallet.getDocument(.init(documentId: documentId))
	                let document = result.record
	                // handle success here
	            } catch {
	                // handle error here
	            }
	        }
	    }
	}
	```

## Delete Document

=== "Android"

    ```kotlin
	launch {
        val result = MobileIdWallet.getInstance().deleteDocument(
            input = DeleteDocument.Input(
                documentId = documentId
            )
        )
    
        if (result.isSuccess) {
            // handle success here
        } else {
            // handle error here
        }
    }
    ```

=== "iOS"

    ```swift
	extension DocumentsManagerSampleUsage {
	    /// Delete document by id
	    func deleteDocument() {
	        Task {
	            do {
	                let documentId = "<YOUR_DOCUMENT_ID>"
	                let result = try await mobileIdWallet.deleteDocument(.init(documentId: documentId))
	                if result.success {
	                    // handle success here
	                } else {
	                    // handle error here
	                }
	            } catch {
	                // handle error here
	            }
	        }
	    }
	}
	```

## Build Document from DocumentReaderReport

We provide a facade method where the developer can convert a DocumentReaderReport into a Document.

=== "Android"

    ```kotlin
    launch {
		val result = MobileIdWallet.getInstance().mapDocumentReaderReportToDocument(
            MapDocumentReaderReportToDocument.Input(documentReaderReport)
        )

		if (result.isSuccess && result.getOrNull()?.success == true) {
            val document = result.getOrNull()?.document
			// TODO handle success here
		} else {
			// TODO handle error here
		}
	}
    ```

=== "iOS"

    ```swift
	extension DocumentsManagerSampleUsage {
	    /// We provide a method where the developer can convert a DocumentReaderReport into a Document.
	    func buildDocument() {
	        let documentReaderReport: DocumentReaderReport = .init(documentData: .init(),
	                                                               idDocument: .init(),
	                                                               documentType: .drivingLicense,
	                                                               documentRFIDStatus: .success,
	                                                               documentStatuses: [],
	                                                               documentPhotoHash: nil,
	                                                               documentDataHash: nil,
	                                                               idDocumentHash: nil)
	        let document: Model.DocumentData = documentReaderReport.mapToDocumentData
	    }
	}
    ```