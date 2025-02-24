# Instalación e implementación gema Pagy

## Agregar la gema pagy al proyecto

```ruby
bundle add pagy
```

## Agregar en el Application Controller app>controller>application_controller.rb para que la gema esté disponible en todos los controladores del desarrollo

```ruby
class ApplicationController < ActionController::Base

  include Pagy::Backend

end
```

## Agregar el helper de pagy en app>helpers>application_helper.rb para que todas las vistas lo hereden

```ruby
module ApplicationHelper

  include Pagy::Frontend

end
```

## Cambiar en el Controller que quiero agregar pagy el metodo index app>controllers>xxxx_controller.rb, en este caso es _posts_controller.rb_


```ruby
  def index
    @posts = Post.order(created_at: :desc) #el post más reciente se muestra primero
  end
```

```ruby
  def index
    @pagy, @posts = pagy(Post.order(created_at: :desc), items: 5) # Paginación
  end
```

## Para agregar estilo Bootstrap al helper hay que crear el archivo pagy.rb en app>config>initializers>pagy.rb y copiar

```ruby
require 'pagy/extras/bootstrap' # Booststrap styling
```

## Agregar el helper al final de la vista index en que se desea mostar la paginación

```ruby
<div class=" d-flex justify-content-center align-items-center">
  <%== pagy_bootstrap_nav(@pagy) %>
</div>
```

## ++++++++++++++ Reiniciar el server ++++++++++++++ 

## Hago commit

```ruby
git add .
git commit -m "Gema pagy instalada y configurada"
```
