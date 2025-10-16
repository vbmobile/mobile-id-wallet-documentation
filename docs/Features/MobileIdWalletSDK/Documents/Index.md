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
	
	class DocumentsManagerSampleUsage {
	    let mobileIdWallet: MobileIdWalletProtocol
	    init(mobileIdWallet: MobileIdWalletProtocol) {
	        self.mobileIdWallet = mobileIdWallet
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
	    func readDocument() {
	        let yourTopViewController: UIViewController = .init()
	        Task {
	            let result = try? await mobileIdWallet.readDocument(.init(viewController: yourTopViewController))
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
	    
	    /// Get/Fetch all the documents
	    func getAllDocuments() {
	        Task {
	            guard let result = try? await mobileIdWallet.getAllDocuments() else { return }
	            print(result.records)
	        }
	    }
	
	    /// Get/Fetch document by id
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
	
	    /// Get/Fetch DocumentReaderReport by id
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