# Document Reader 

This SDK supports a wide range of passports and boarding passes, enabling seamless document reading and verification. By leveraging advanced OCR and NFC technologies, it ensures accurate data extraction from various document formats worldwide.

With built-in camera integration, the SDK provides a smooth scanning experience, requiring only a base view controller to trigger the document capture. Whether you're handling passport-based identity verification or boarding pass processing, the SDK streamlines the process with high reliability and performance.maintainable.

## Read Passport

=== "Android"

    ```kotlin
        ...
    ```

=== "iOS"

    ```swift
	import MobileIdWalletSDK
	import WalletSDKCore
	
	class DocumentReader {
	    let mobileIdWallet: MobileIdWalletProtocol
	    init(mobileIdWallet: MobileIdWalletProtocol) {
	        self.mobileIdWallet = mobileIdWallet
	    }
	}
	
	extension DocumentReader {
	    func readPassportDocument() async {
	        /// The `viewController` is required because the SDK needs a base view controller
	        /// to present the camera interface for document scanning. This should be the
	        /// screen from which the SDK is invoked.
	        let viewController = UIViewController()
	        try? await mobileIdWallet.readDocument(.init(viewController: viewController, type: .passport))
	    }
	}
    ```


## Read Boarding Pass

=== "Android"

    ```kotlin
        ...
    ```

=== "iOS"

    ```swift
	import MobileIdWalletSDK
	import WalletSDKCore
	
	class DocumentReader {
	    let mobileIdWallet: MobileIdWalletProtocol
	    init(mobileIdWallet: MobileIdWalletProtocol) {
	        self.mobileIdWallet = mobileIdWallet
	    }
	}
	
	extension DocumentReader {
	    func readBoardingPass() async {
	        /// The `viewController` is required because the SDK needs a base view controller
	        /// to present the camera interface for document scanning. This should be the
	        /// screen from which the SDK is invoked.
	        let viewController = UIViewController()
	        try? await mobileIdWallet.readDocument(.init(viewController: viewController, type: .boardingPass))
	    }
	}

    ```