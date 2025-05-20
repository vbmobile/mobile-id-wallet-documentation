# Document Reader 

This SDK supports a wide range of passports and boarding passes, enabling seamless document reading and verification. By leveraging advanced OCR and NFC technologies, it ensures accurate data extraction from various document formats worldwide.

With built-in camera integration, the SDK provides a smooth scanning experience, requiring only a base view controller to trigger the document capture. Whether you're handling passport-based identity verification or boarding pass processing, the SDK streamlines the process with high reliability and performance.

## Read Passport

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
	import MobileIdWalletSDK
	import WalletSDKCore
	import UIKit
	import Foundation
	
	class DocumentReader {
	    let mobileIdWallet: MobileIdWalletProtocol
	    init(mobileIdWallet: MobileIdWalletProtocol) {
	        self.mobileIdWallet = mobileIdWallet
	    }
	}
	
	extension DocumentReader {
	    func readPassportDocument() {
	        /// The `viewController` is required because the SDK needs a base view controller
	        /// to present the camera interface for document scanning. This should be the
	        /// screen from which the SDK is invoked.
	        let viewController = UIViewController()
	        Task {
	            let ouput = try? await mobileIdWallet.readDocument(.init(viewController: viewController, type: .passport))
	            guard let passportData = ouput?.document as? Model.PassportData else { return }
	            print(passportData)
	        }
	    }
	}
    ```


## Read Boarding Pass

=== "Android"

    ```kotlin
	MobileIdWallet.getInstance().readBoardingPass(
		activity = requireActivity(),
		params = BoardingPassParameters(false),
		onScanBoardingPassCompletion = object : OnScanBoardingPassCompletion {
			override fun onBoardingPassError(boardingPassError: BoardingPassError) {
				
			}

			override fun onBoardingPassSuccess(boardingPass: BoardingPass) {
				
			}
		}
	)
    ```

=== "iOS"

    ```swift
	import MobileIdWalletSDK
	import WalletSDKCore
	import UIKit
	import Foundation
	
	class DocumentReader {
	    let mobileIdWallet: MobileIdWalletProtocol
	    init(mobileIdWallet: MobileIdWalletProtocol) {
	        self.mobileIdWallet = mobileIdWallet
	    }
	}
	
	extension DocumentReader {
	    func readBoardingPass() {
	        /// The `viewController` is required because the SDK needs a base view controller
	        /// to present the camera interface for document scanning. This should be the
	        /// screen from which the SDK is invoked.
	        let viewController = UIViewController()
	        Task {
	            let ouput = try? await mobileIdWallet.readDocument(.init(viewController: viewController, type: .boardingPass))
	            guard let boardingPass = ouput?.document as? Model.BoardingPass else { return }
	            print(boardingPass)
	        }
	    }
	}

    ```