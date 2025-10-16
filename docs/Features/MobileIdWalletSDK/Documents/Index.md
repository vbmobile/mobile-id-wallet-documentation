# Document Reader 

The Mobile ID Wallet SDK provides comprehensive support for managing identity documents within the wallet. Developers can retrieve all stored documents or access a specific document by its unique identifier. Documents can be added to the wallet by capturing them with the device camera and optionally using RFID for enhanced security. Stored documents can also be deleted when no longer needed. 

All operations support Swift’s async/await concurrency model, with optional completion handler alternatives for traditional callback-based workflows. Strongly typed input and output models ensure safe and predictable access to document data, while the API maintains a consistent Swift-native style for seamless integration into your app.


## Setup

=== "Android"

    ```kotlin
	 TO DO    
    ```
    
=== "iOS"

    ```swift
	import Foundation
	import WalletSDKCore
	import MobileIdWalletSDK
	import MobileIdSDKiOS // MobileID (VB Enrollment SDK)
	
	class DocumentsManagerSampleUsage {
	    let mobileIdWallet: MobileIdWalletProtocol
	    init(mobileIdWallet: MobileIdWalletProtocol) {
	        self.mobileIdWallet = mobileIdWallet
	    }
	
	    init(input: MobileIdWalletSetup.Input) {
	        self.mobileIdWallet = MobileIdWallet.shared
	        mobileIdWallet.setup(.init(mobileIdWalletConfig: input.mobileIdWalletConfig))
	    }
	}
	```

## Read

=== "Android"

    ```kotlin
    MobileIdWallet.getInstance().readDocument(
		activity = requireActivity(),
		params = DocumentReaderParameters(true),
		onReadDocumentCompletion = object : OnReadDocumentCompletion {
			override fun onReadDocumentError(documentReaderError: DocumentReaderError) {
				
			}

			override fun onReadDocumentSuccess(document: Document) {
				
			}
		}
	)
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
	TO DO
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
	
	    /// Retrieves a specific document from the wallet using its unique identifier.
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
	
	    /// Retrieves a specific document from the wallet using its unique identifier.
	    func getDocumentReaderReportById() {
	        Task {
	            let documentId = "your_document_id"
	            let getDocumentOutput = try? await mobileIdWallet.getDocument(.init(documentId: documentId))
	            guard let document = getDocumentOutput?.record else {
	                return
	            }
	            if let documentReaderReport = document.documentReaderReport {
	                print(documentReaderReport)
	            }
	        }
	    }
	}
    ```

## Delete Document

=== "Android"

    ```kotlin
	TO DO
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