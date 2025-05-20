# Intro

![Alt Text](Assets/SampleUsage1.gif)

MobileIdWalletUISDK simplifies navigation by providing a pre-built UI and routing system. Developers only need to decide where to direct users within the SDK, without manually handling view controller transitions.

The MobileIdWalletUIRouterProtocol handles routing to key sections, such as the Verifiable Credentials and Flights screens. Below is a sample implementation:

## Sample Usage

=== "Android"

	To create a trip, call the following facade method:

    ```kotlin
    MobileIdWalletUI.getInstance().createTrip(requireActivity())
    ```

	To show the credentials list screen, call the following facade method:

	```kotlin
	MobileIdWalletUI.getInstance().showDigitalIds(requireActivity())
	```

	To show the boarding passes list screen, call the following facade method:

	```kotlin
	MobileIdWalletUI.getInstance().showTrips(requireActivity())
	```

=== "iOS"



	```swift
	import UIKit
	import MobileIdWalletUISDK
	
	class RoutingExampleViewController: UIViewController {
	    let router: MobileIdWalletUIRouterProtocol?
	    public init(router: MobileIdWalletUIRouterProtocol?) {
	        self.router = router
	        super.init(nibName: nil, bundle: nil)
	    }
	
	    @available(*, unavailable)
	    required init?(coder: NSCoder) {
	        fatalError("init(coder:) has not been implemented")
	    }
	
	    override func viewDidLoad() {
	        super.viewDidLoad()
	        view.backgroundColor = .white
	
	        let btnAccessWallet = UIButton(type: .system)
	        btnAccessWallet.setTitle("Access digital ID Wallet", for: .normal)
	        btnAccessWallet.addTarget(self, action: #selector(btnAccessWalletTapped), for: .touchUpInside)
	
	        let btnCreateTrip = UIButton(type: .system)
	        btnCreateTrip.setTitle("Route to trips", for: .normal)
	        btnCreateTrip.addTarget(self, action: #selector(btnCreateTripTapped), for: .touchUpInside)
	
	        let stackView = UIStackView(arrangedSubviews: [btnAccessWallet, btnCreateTrip])
	        stackView.axis = .vertical
	        stackView.spacing = 16
	        stackView.translatesAutoresizingMaskIntoConstraints = false
	
	        view.addSubview(stackView)
	
	        NSLayoutConstraint.activate([
	            stackView.centerXAnchor.constraint(equalTo: view.centerXAnchor),
	            stackView.centerYAnchor.constraint(equalTo: view.centerYAnchor)
	        ])
	    }
	
	    @objc private func btnAccessWalletTapped() {
	        router?.navigateToVerifiableCredentials(model: .init())
	    }
	
	    @objc private func btnCreateTripTapped() {
	        router?.navigateToFlights(model: .init(shouldCreateNewOnScreenLoad: false))
	    }
	}
	```

