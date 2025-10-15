# Document Reader 

This SDK supports a wide range of passports and boarding passes, enabling seamless document reading and verification. By leveraging advanced OCR and NFC technologies, it ensures accurate data extraction from various document formats worldwide.

With built-in camera integration, the SDK provides a smooth scanning experience, requiring only a base view controller to trigger the document capture. Whether you're handling passport-based identity verification or boarding pass processing, the SDK streamlines the process with high reliability and performance.

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
	
	class ManageDocuments {
	    let mobileIdWallet: MobileIdWalletProtocol
	    init(mobileIdWallet: MobileIdWalletProtocol) {
	        self.mobileIdWallet = mobileIdWallet
	    }
	}
	```

## Read Document

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
	extension ManageDocuments {
	    func readDocument() {
	        Task {
	            let output = try? await mobileIdWallet.readDocument(.init(viewController: UIViewController()))
	            guard let document = output?.document else {
	                return
	            }
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
	extension ManageDocuments {
	    func getAllDocuments() {
	        Task {
	            /// Fetch all the documents
	            guard let output = try? await mobileIdWallet.getAllDocuments() else {
	                return
	            }
	            print(output.records)
	        }
	    }
	
	    func getDocument() {
	        Task {
	            guard let getAllDocumentsOutput = try? await mobileIdWallet.getAllDocuments(),
	                  let document = getAllDocumentsOutput.records.first else {
	                return
	            }
	            let getDocumentOutput = try? await mobileIdWallet.getDocument(.init(documentId: document.id))
	            if let document = getDocumentOutput?.record {
	                print(document)
	                print(document.documentReaderReport as Any)
	            }
	        }
	    }
	
	    func getDocumentReaderReport() {
	        Task {
	            guard let getAllDocumentsOutput = try? await mobileIdWallet.getAllDocuments(),
	                  let document = getAllDocumentsOutput.records.first else {
	                return
	            }
	            let getDocumentOutput = try? await mobileIdWallet.getDocument(.init(documentId: document.id))
	            if let documentReaderReport = getDocumentOutput?.record.documentReaderReport {
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
	extension ManageDocuments {
	    func deleteDocument() {
	        Task {
	            guard let output = try? await mobileIdWallet.getAllDocuments(),
	                  let document = output.records.first else {
	                return
	            }
	            let deleteDocumentOutput = try? await mobileIdWallet.deleteDocument(.init(documentId: document.id))
	            if let success = deleteDocumentOutput?.success {
	                print("success: \(success)")
	            }
	        }
	    }
	}
	```