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
	
	class ManageBoardingPasses {
	    let mobileIdWallet: MobileIdWalletProtocol
	    init(mobileIdWallet: MobileIdWalletProtocol) {
	        self.mobileIdWallet = mobileIdWallet
	    }
	}
	```

## Read or Scan

=== "Android"

    ```kotlin
	TO DO
    ```

=== "iOS"

    ```swift
	extension ManageBoardingPasses {
	    func scanBoardingPass() {
	        let viewController = UIViewController()
	        Task {
	            try? await mobileIdWallet.scanBoardingPass(.init(viewController: viewController, parameters: .defaultParameters()))
	        }
	    }
	
	    func parseBoardingPass() {
	        let viewController = UIViewController()
	        Task {
	            try? await mobileIdWallet.parseBoardingPass(.init(viewController: viewController, parameters: .defaultParameters(image: UIImage())))
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
	extension ManageBoardingPasses {
	    func getAllBoardingPass() async {
	        Task {
	            let output = try? await mobileIdWallet.getAllBoardingPass()
	            if let records = output?.records {
	                print(records)
	            }
	        }
	    }
	
	    func getBoardingPass() async {
	        guard let fetchAllBoardingPassOutput = try? await mobileIdWallet.getAllBoardingPass(),
	              let boardingPassId = fetchAllBoardingPassOutput.records.first?.id else { return }
	        let output = try? await mobileIdWallet.getBoardingPass(.init(boardingPassId: boardingPassId))
	        guard let boardingPass = output?.record else { return }
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
	extension ManageBoardingPasses {
	    func deleteBoardingPass() async {
	        guard let fetchAllBoardingPassOutput = try? await mobileIdWallet.getAllBoardingPass(),
	              let boardingPassId = fetchAllBoardingPassOutput.records.first?.id else { return }
	        _ = try? await mobileIdWallet.deleteBoardingPass(.init(boardingPassId: boardingPassId))
	    }
	}
	```
	
## Sample

=== "Android"

    ```kotlin
	TO DO
    ```

=== "iOS"

    ```swift
	TO DO
	```
	
