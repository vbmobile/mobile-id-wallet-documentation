# Boarding Passes

This SDK provides full CRUD support for boarding passes, allowing you to create, read, update, and delete them with ease. By integrating boarding pass data with verifiable credentials, the SDK enhances the airport experience, enabling smoother check-ins, security screenings, and boarding processes.

With built-in scanning capabilities, the SDK extracts key information from a wide range of boarding passes, ensuring seamless integration with digital identity solutions. By linking a boarding pass to a verifiable credential, travelers can experience faster verification and reduced friction throughout their journey.

## Fetch all Boarding Pass

=== "Android"

    ```kotlin
    launch {
		val result = MobileIdWallet.getInstance().getAllBoardingPass()
		
		if (result.isSuccess) {
			val boardingPasses = result.getOrNull()?.records
			// TODO handle success here
		} else {
			// TODO handle error here
		}
	}
    ```

=== "iOS"

    ```swift
	import MobileIdWalletSDK
	import Foundation
	import UIKit
	
	class ManageBoardingPasses {
	    let mobileIdWallet: MobileIdWalletProtocol
	    init(mobileIdWallet: MobileIdWalletProtocol) {
	        self.mobileIdWallet = mobileIdWallet
	    }
	}
	
	extension ManageBoardingPasses {
	    func getAllBoardingPass() async {
	        Task {
	            let output = try? await mobileIdWallet.getAllBoardingPass(.init())
	            print(output?.records ?? [])
	        }
	    }
	}

    ```


## Get Boarding Pass

=== "Android"

    ```kotlin
    launch {
		val result = MobileIdWallet.getInstance().getAllBoardingPass(
			input = GetAllBoardingPass.Input(
				boardingPassId = boardingPassId
			)
		)

		if (result.isSuccess) {
			val boardingPasse = result.getOrNull()?.boardingPass
			// TODO handle success here
		} else {
			// TODO handle error here
		}
	}
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
	    func getBoardingPass() async {
	        guard let fetchAllBoardingPassOutput = try? await mobileIdWallet.getAllBoardingPass(.init()),
	              let boardingPassId = fetchAllBoardingPassOutput.records.first?.id else { return }
	        let output = try? await mobileIdWallet.getBoardingPass(.init(boardingPassId: boardingPassId))
	        guard let boardingPass = output?.record else { return }
	        print(boardingPass)
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
	import Foundation
	
	class ManageBoardingPasses {
	    let mobileIdWallet: MobileIdWalletProtocol
	    init(mobileIdWallet: MobileIdWalletProtocol) {
	        self.mobileIdWallet = mobileIdWallet
	    }
	}
	
	extension ManageBoardingPasses {
	    func readBoardingPass() {
	        /// The `viewController` is required because the SDK needs a base view controller
	        /// to present the camera interface for document scanning. This should be the
	        /// screen from which the SDK is invoked.
	        let viewController = UIViewController()
	        Task {
	            try? await mobileIdWallet.readBoardingPass(.init(viewController: viewController))
	        }
	    }
    }
    ```
    
## Associate Boarding Pass with Verifiable Credential

=== "Android"

    ```kotlin
    launch {
		val result = MobileIdWallet.getInstance().assocBoardingPassWithCredential(
			context = requireActivity(),
			input = AssocBoardingPassWithCredential.Input(
				credentialId = credentialId,
				boardingPassId = boardingPassId,
				requiresAuthenticationToCompleteFlow = true
			)
		)

		if (result.isSuccess && result.getOrNull()?.success == true) {
			// TODO handle success here
		} else {
			// TODO handle error here
		}
	}
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
	    func assocBoardingPassWithCredential() {
	        /// The `viewController` is required because the SDK needs a base view controller
	        /// to present the camera interface for face scanning. This should be the
	        /// screen from which the SDK is invoked.
	        let viewController = UIViewController()
	        Task {
	            guard let output = try? await mobileIdWallet.fetchAllBoardingPass(.init()),
	                  let boardingPassId = output.records.first?.id else { return }
	
	            guard let output = try? await mobileIdWallet.fetchAllCredentials(.init()),
	                  let credentialId = output.records.first?.id else { return }
	
	            _ = try? await mobileIdWallet.assocBoardingPassWithCredential(.init(
	                viewController: viewController,
	                credentialId: credentialId,
	                boardingPassId: boardingPassId,
	                requiresAuthenticationToCompleteFlow: true
	            ))
	        }
	    }
	}
    ```