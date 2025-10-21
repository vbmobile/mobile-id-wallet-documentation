# Document Reader

The Mobile ID Wallet SDK provides comprehensive support for managing identity documents within the
wallet. Developers can retrieve all stored documents or access a specific document by its unique
identifier. Documents can be added to the wallet by capturing them with the device camera and
optionally using RFID for enhanced security. Stored documents can also be deleted when no longer
needed.

All operations support Swift’s async/await concurrency model, with optional completion handler
alternatives for traditional callback-based workflows. Strongly typed input and output models ensure
safe and predictable access to document data, while the API maintains a consistent Swift-native
style for seamless integration into your app.

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
	            let result = try? await mobileIdWallet.readDocument(.init(
	                viewController: yourTopViewController,
	                readDocumentParameters: parameters
	            ))
	            guard let document = result?.document else { return }
	            print(document)
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
	            guard let result = try? await mobileIdWallet.getAllDocuments() else { return }
	            print(result.records)
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
    func getDocumentById() {
        Task {
            let documentId = "your_document_id"
            let getDocumentOutput = try? await mobileIdWallet.getDocument(.init(documentId: documentId))
            guard let document = getDocumentOutput?.record else {
                return
            }
            print(document)
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
	            let documentId = "your_document_id"
	            let result = try? await mobileIdWallet.deleteDocument(.init(documentId: documentId))
	            if let success = result?.success {
	                print("success: \(success)")
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
    TODO
    ```