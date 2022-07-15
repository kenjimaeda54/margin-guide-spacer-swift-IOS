# Margin Guide and Spacer
Praticando conceito de margin and spacer no IOS


## Feature
- Para criar botão com espaçamento interno baseado na fonte  precisa usar método configuration e o objeto filled
- Criei minhas próprias cores com extension UIColor
- Ideia abaixo e realizar um espacamento igual entre os botões ,parecido com space-evenly do flex box
- Segredo e adicionar objeto UILayoutGuide 


```swift
**
import UIKit

class ViewController: UIViewController {
	
	override func viewDidLoad() {
		super.viewDidLoad()
		setupViews()
	}
	
	func setupViews() {
		let buttonOk = makeButton("Ok", UIColor.darkBlue)
		let buttonCancel = makeButton("Cancel", UIColor.darkGreen)
		let guideOk = UILayoutGuide()
		let guideCancel = UILayoutGuide()
		let middleGuide = UILayoutGuide()
		
		view.addSubview(buttonOk)
		view.addSubview(buttonCancel)
		view.addLayoutGuide(guideOk)
		view.addLayoutGuide(guideCancel)
		view.addLayoutGuide(middleGuide)
		
		//setup contraint
		let margin = view.layoutMarginsGuide
		
		NSLayoutConstraint.activate([
			//leading  guide
			margin.leadingAnchor.constraint(equalTo: guideOk.leadingAnchor),
			guideOk.trailingAnchor.constraint(equalTo: buttonOk.leadingAnchor),
			
			//middle guide
			buttonOk.trailingAnchor.constraint(equalTo: middleGuide.leadingAnchor),
			middleGuide.trailingAnchor.constraint(equalTo: buttonCancel.leadingAnchor),
			
			
			//trailing guide
			buttonCancel.trailingAnchor.constraint(equalTo: guideCancel.leadingAnchor),
			guideCancel.trailingAnchor.constraint(equalTo: margin.trailingAnchor),
			
			
			//button equal widths
			buttonCancel.widthAnchor.constraint(equalTo: buttonOk.widthAnchor),
			
			// spacer equal widths
			guideOk.widthAnchor.constraint(equalTo: guideCancel.widthAnchor),
			guideOk.widthAnchor.constraint(equalTo: middleGuide.widthAnchor),
			
			
			//vertical position
			buttonOk.centerYAnchor.constraint(equalTo: view.centerYAnchor),
			buttonCancel.centerYAnchor.constraint(equalTo: view.centerYAnchor),
			guideOk.centerYAnchor.constraint(equalTo: view.centerYAnchor),
			guideCancel.centerYAnchor.constraint(equalTo: view.centerYAnchor),
			middleGuide.centerYAnchor.constraint(equalTo: view.centerYAnchor),
			
			//height position
			guideOk.heightAnchor.constraint(equalToConstant: 1),
			guideCancel.heightAnchor.constraint(equalToConstant: 1),
			middleGuide.heightAnchor.constraint(equalToConstant: 1)
		])
		
		
		
		
	}
	
	func makeButton(_ text: String,_ color: UIColor) -> UIButton {
		//https://stackoverflow.com/questions/68328038/imageedgeinsets-was-deprecated-in-ios-15-0
		let button = UIButton()
		var configuration =  UIButton.Configuration.filled()
		button.translatesAutoresizingMaskIntoConstraints = false
		button.setTitle(text, for: .normal)
		button.setTitleColor(.white, for: .normal)
		configuration.baseBackgroundColor = color
		//ajustar fonte de acordo com o botao
		button.titleLabel?.adjustsFontSizeToFitWidth = true
		//aqui e titlePadding  nos label
		configuration.titlePadding = 5
		//contentInsets e o padding interno do button
		configuration.contentInsets = NSDirectionalEdgeInsets(top: 8,leading: 16,bottom: 8,trailing:16 )
		button.configuration = configuration
		return button
	}
	
	
}
extension UIColor  {
	//maneira de fazer rgba
	static let darkBlue = UIColor(red: 10/255,green: 133/255, blue: 255/255,alpha: 1)
	static let darkGreen = UIColor(red: 48/255,green: 209/255, blue: 88/255,alpha: 1)
}**




```
