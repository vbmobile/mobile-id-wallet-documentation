# Boarding Passes

This SDK provides full CRUD support for boarding passes, allowing you to create, read, update, and delete them with ease. By integrating boarding pass data with verifiable credentials, the SDK enhances the airport experience, enabling smoother check-ins, security screenings, and boarding processes.

With built-in scanning capabilities, the SDK extracts key information from a wide range of boarding passes, ensuring seamless integration with digital identity solutions. By linking a boarding pass to a verifiable credential, travelers can experience faster verification and reduced friction throughout their journey.


## Setup

=== "Android"

    ```kotlin
	TO DO
    ```

=== "iOS"

    ```swift
	import MobileIdWalletSDK
	import Foundation
	import UIKit
	
	class BoardingPassManagerSampleUsage {
	    let mobileIdWallet: MobileIdWalletProtocol
	    init(mobileIdWallet: MobileIdWalletProtocol) {
	        self.mobileIdWallet = mobileIdWallet
	    }
	}
	```

## Parse/Scan

=== "Android"

    ```kotlin
	TO DO
    ```

=== "iOS"

    ```swift
	extension BoardingPassManagerSampleUsage {
	    /// Scan boarding pass using the device camera
	    func scanBoardingPass() {
	        let viewController = UIViewController()
	        Task {
	            /// Scan boarding pass using the device camera
	            try? await mobileIdWallet.scanBoardingPass(.init(
	                viewController: viewController,
	                parameters: .init(validateBoardingPass: true)
	            ))
	        }
	    }
	
	    /// Parse boarding pass providing a picture of the boarding pass
	    func parseBoardingPass() {
	        let viewController = UIViewController()
	        let boardingPassImage = UIImage()
	        Task {
	            /// Parse boarding pass providing a picture of the boarding pass
	            try? await mobileIdWallet.parseBoardingPass(.init(
	                viewController: viewController,
	                parameters: .init(validateBoardingPass: true, boardingPassData: nil, boardingPassImage: boardingPassImage)
	            ))
	        }
	    }
	}
	```
	
## Get/Fetch 

=== "Android"

    ```kotlin
	TO DO
    ```

=== "iOS"

    ```swift
	extension BoardingPassManagerSampleUsage {
	    /// Get/Fetch all stored boading passes
	    func getAllBoardingPass() async {
	        Task {
	            let result = try? await mobileIdWallet.getAllBoardingPass()
	            print(result?.records ?? [])
	        }
	    }
	
	    /// Get/Fetch boarding pass by id
	    func getBoardingPassById() async {
	        let boardingPassId = "your_boarding_pass_id"
	        let result = try? await mobileIdWallet.getBoardingPass(.init(boardingPassId: boardingPassId))
	        guard let boardingPass = result?.record else { return }
	        print(boardingPass)
	    }
}
	```
	
## Delete

=== "Android"

    ```kotlin
	TO DO
    ```

=== "iOS"

    ```swift
	extension BoardingPassManagerSampleUsage {
	    /// Delete boarding pass by id
	    func deleteBoardingPass() async {
	        let boardingPassId = "your_boarding_pass_id"
	        _ = try? await mobileIdWallet.deleteBoardingPass(.init(boardingPassId: boardingPassId))
	    }
	}
	```
