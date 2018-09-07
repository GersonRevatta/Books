# Rails Mailer
Es el componente que se encarga de envios de correos en rails; el primer paso para poder mandar correos en Rails es crear un mailer
## Example
####Nota: Este tutorial considera que se has hecho la configuracion
### Contact form
Tenemos que crear un controller para que procese la peticion, y su respectiva ruta
```
rails g controller contacts
match '/send_mail', to: 'contacts#send_mail', via: 'post'
```
Asi queda el controller
```
class ContactsController < ApplicationController
  def send_mail
    name = params[:name]
    email = params[:email]
    body = params[:comments]
    redirect_to root_path, notice: 'Message sent'
  end
end
```
Luego se crea un partial form, para insertar el contact form donde desees
```
<%= form_tag(send_mail_path) do %>
  <div class="form-group">
    <%= label_tag 'name', 'Name' %>
    <%= text_field_tag 'name', nil, class: 'form-control', placeholder: 'Your Name' %>
  </div>
  <div class="form-group">
    <%= label_tag 'email', 'Email' %>
    <%= email_field_tag 'email', nil, class: 'form-control', placeholder: 'Your Email Address' %>
  </div>
  <div class="form-group">
    <%= label_tag 'comments', 'Comments' %>
    <%= text_area_tag 'comments', nil, class: 'form-control', rows: 4, placeholder: 'Comments...' %>
  </div>
  <%= submit_tag nil, class: 'btn btn-default btn-about pull-right' %>
 <% end %>

```
Ahora generaremos el mailer
```
rails g mailer contact
```
Esto generara un file en mailer y tambien en views
Vamos a /mailers/contact_mailer.rb, agregamos los campos correspondientes
```
  def contact_email(name, email, body)
      @name = name
      @email = email
      @body = body
      mail(to:'your@email.com',from: email, subject: 'Contact Request')
  end
```
Luego a la views del mailer generado, creamos  contact_email.html.erb , tambien contact_email.text.erb( ya que no puede ser soportado el html en el mensaje) para este caso sera asi, Esto sera el cuerpo del mensaje 
```
HTML
<h1>Pregunta de  <%= @name %></h1>
<p><%= @email %></p>
<p>El mensaje es: <%= @body %></p>
<p>Thanks for joining and have a great day!</p>
TEXT
Welcome to example.com,
===============================================

You have successfully signed up to example.com,
your username is: 

Thanks for joining and have a great day!
```
Luego llamamos el mailer desde el controller, quedaria asi
```
class ContactsController < ApplicationController
  def send_mail
    name = params[:name]
    email = params[:email]
    body = params[:comments]
    ContactMailer.contact_email(name, email, body).deliver
    redirect_to root_path, notice: 'Message sent'
  end
end

```