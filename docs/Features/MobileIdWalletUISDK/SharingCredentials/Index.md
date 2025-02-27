# Sharing Credentials

Verifiable credentials (VCs) provide a secure, tamper-proof way to issue, share, and verify digital credentials. When sharing or presenting a credential, users can selectively disclose information based on the verifier's request. This means they can prove specific claims (e.g., age or membership) without exposing unrelated details. The process typically involves cryptographic proofs, ensuring authenticity while preventing forgery or unauthorized modifications. VCs also support privacy-preserving techniques like zero-knowledge proofs, allowing users to confirm a fact without revealing the underlying data. This makes credential sharing both secure and user-controlled across various digital interactions.

## Sharing credentials using Deep linking

=== "Android"

    ```kotlin
        ...
    ```

=== "iOS"

	```swift
	import UIKit
	import WalletSDKCommon
	import MobileIdWalletUISDK
	import MobileIdWalletSDK
	
	@main
	class AppDelegate: UIResponder, UIApplicationDelegate {
	    var window: UIWindow? // Declare the window property
	    var deeplinkManager: DeeplinkManager?
	    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
	        _ = applicationDefault(application, didFinishLaunchingWithOptions: launchOptions)
	        /* Your initial step goes here */
	        return true
	    }
	
	    func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey: Any] = [:]) -> Bool {
	        if let scheme = url.scheme, scheme == "openid-vc" {
	            // Init the DeeplinkManager (if needed) with the reference to you MobileIdWallet(Protocol) instance
	            if deeplinkManager == nil {
	                let yourMobileIdWalletReference: MobileIdWalletProtocol = DependenciesResolver.shared.mobileIdWallet
	                deeplinkManager = DeeplinkManager(mobileIdWallet: yourMobileIdWalletReference)
	            }
	            deeplinkManager?.handleWithUI(url: url)
	            return true
	        }
	        return false
	    }	
	}
	```
	
    ```swift
	import MobileIdWalletSDK
	import Foundation
	
	class DeeplinkManager {
	    let mobileIdWallet: MobileIdWalletProtocol
	    init(mobileIdWallet: MobileIdWalletProtocol) {
	        self.mobileIdWallet = mobileIdWallet
	    }
	}
	
	extension DeeplinkManager {
	    func handleWithUI(url: URL) {
	        DispatchQueue.main.asyncAfter(deadline: .now() + 1) { [weak self] in
	            guard let self else { return }
	            // Step 1 - Validate URL
	            guard let scheme = url.scheme, scheme == "openid-vc" else {
	                // Invalid URL
	                return
	            }
	            // Step 2 - Pick top View controler
	            let topViewController = UIApplication.shared.connectedScenes
	                .filter { $0.activationState == .foregroundActive }
	                .map { $0 as? UIWindowScene }
	                .first??.windows.first?.rootViewController
	            guard let topViewController else {
	                print("Fail to get top view controller")
	                return
	            }
	            // Step 3 - Setup the MobileIdWalletUIRouter with the topViewController
	            walletUIRouter.setup(rootViewController: topViewController)
	            // Step 4 - Ordering the router do navigator to the screen
	            // where we will choose the credential to share (if any credential is stored)
	            walletUIRouter.navigateToCredentialPicker(model: .init(records: [], url: url.absoluteString))
	        }
	    }	
    }
    ```

