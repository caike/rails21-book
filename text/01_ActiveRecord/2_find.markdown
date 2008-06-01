## Find

### Conditions

A partir de agora é possível passar um objeto como parâmetro no método **find** de uma classe **ActiveRecord**. Veja este caso como exemplo:

	class Account < ActiveRecord::Base
	  composed_of :balance, :class_name => “Money”, :mapping => %w(balance amount)
	end

Nesse caso, você pode passar um objeto Money como parâmetro no método find da classe Account, assim:

	amount = 500
	currency = “USD”
	Account.find(:all, :conditions => { :balance => Money.new(amount, currency) })
	
### Last

Até agora podíamos usar apenas três operadores para procurar dados usando o método **find** do **ActiveRecord**: **:first**, **:all** e o próprio id do objeto (neste caso não usamos um operador especifico, mas a falta de um significa que estamos passando o id).

Agora teremos um quarto operador o **:last**. Veja alguns exemplos:

	Person.find(:last)
	Person.find(:last, :conditions => [ "user_name = ?", user_name])
	Person.find(:last, :order => “created_on DESC“, :offset => 5)