# Boarding Passes

This SDK provides full CRUD support for boarding passes, allowing you to create, read, update, and delete them with ease. By integrating boarding pass data with verifiable credentials, the SDK enhances the airport experience, enabling smoother check-ins, security screenings, and boarding processes.

With built-in scanning capabilities, the SDK extracts key information from a wide range of boarding passes, ensuring seamless integration with digital identity solutions. By linking a boarding pass to a verifiable credential, travelers can experience faster verification and reduced friction throughout their journey.

## Fetch all Boarding Pass

=== "Android"

    ```kotlin
        ...
    ```

=== "iOS"

    ```swift
	import MobileIdWalletSDK
	import Foundation
	
	class ManageBoardingPasses {
	    let mobileIdWallet: MobileIdWalletProtocol
	    init(mobileIdWallet: MobileIdWalletProtocol) {
	        self.mobileIdWallet = mobileIdWallet
	    }
	}
	
	extension ManageBoardingPasses {
	    func fetchAllBoardingPass() async {
	        try? await mobileIdWallet.fetchAllBoardingPass(.init())
	    }
	}
    ```


## Fetch Boarding Pass

=== "Android"

    ```kotlin
        ...
    ```

=== "iOS"

    ```swift
	import MobileIdWalletSDK
	import Foundation
	
	class ManageBoardingPasses {
	    let mobileIdWallet: MobileIdWalletProtocol
	    init(mobileIdWallet: MobileIdWalletProtocol) {
	        self.mobileIdWallet = mobileIdWallet
	    }
	}
	
	extension ManageBoardingPasses {
	    func fetchBoardingPass() async {
	        guard let output = try? await mobileIdWallet.fetchAllBoardingPass(.init()),
	        let boardingPassId = output.records.first?.id else { return }
	        try? await mobileIdWallet.fetchBoardingPass(.init(boardingPassId: boardingPassId))
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
	import Foundation
	
	class ManageBoardingPasses {
	    let mobileIdWallet: MobileIdWalletProtocol
	    init(mobileIdWallet: MobileIdWalletProtocol) {
	        self.mobileIdWallet = mobileIdWallet
	    }
	}
	
	extension ManageBoardingPasses {
	    func readDocumentBoardingPass() async {
	        /// The `viewController` is required because the SDK needs a base view controller
	        /// to present the camera interface for document scanning. This should be the
	        /// screen from which the SDK is invoked.
	        let viewController = UIViewController()
	        try? await mobileIdWallet.readDocument(.init(viewController: viewController, type: .boardingPass))
	    }
	}
    ```
    
## Associate Boarding Pass with Verifiable Credential

=== "Android"

    ```kotlin
        ...
    ```

=== "iOS"

    ```swift
	import MobileIdWalletSDK
	import Foundation
	
	class ManageBoardingPasses {
	    let mobileIdWallet: MobileIdWalletProtocol
	    init(mobileIdWallet: MobileIdWalletProtocol) {
	        self.mobileIdWallet = mobileIdWallet
	    }
	}
	
	extension ManageBoardingPasses {
	    func assocBoardingPassWithCredential() async {
	        guard let output = try? await mobileIdWallet.fetchAllBoardingPass(.init()),
	        let boardingPassId = output.records.first?.id else { return }
	        
	        guard let output = try? await mobileIdWallet.fetchAllCredentials(.init()),
	        let credentialId = output.records.first?.id else { return }
	        
	        /// The `viewController` is required because the SDK needs a base view controller
	        /// to present the camera interface for face scanning. This should be the
	        /// screen from which the SDK is invoked.
	        let viewController = UIViewController()
	        try? await mobileIdWallet.assocBoardingPassWithCredential(.init(viewController: viewController,
	                                                                        credentialId: credentialId,
	                                                                        boardingPassId: boardingPassId,
	                                                                        requiresAuthenticationToCompleteFlow: true))
	    }
	}
    ```