TDD and BDD
  Desarrollo guiado por pruebas de software, o Test-driven development (TDD) 
  En primer lugar, se escribe una prueba y se verifica que las pruebas fallan. A continuación, se implementa el código que hace que la prueba pase satisfactoriamente y seguidamente se refactoriza el código escrito. El propósito del desarrollo guiado por pruebas es lograr un código limpio que funcione. La idea es que los requisitos sean traducidos a pruebas, de este modo, cuando las pruebas pasen se garantizará que el software cumple con los requisitos que se han establecido. 

  Aprender bien el ciclo  del TDD
  https://es.wikipedia.org/wiki/Desarrollo_guiado_por_pruebas



  Crear mi db para mis pruebas
  rake db:create RAILS_ENV=test
  rake db:migrate RAILS_ENV=test

 RAILS_ENV=test rails c




  code should-matcher
  
require 'rails_helper'
RSpec.describe Category, type: :model do
  it { should belong_to(:department) }
  it { should validate_presence_of(:content) }
  it { should have_many(:themes) }
  it { should have_many(:levels) }
  it { should validate_presence_of(:name) }
end
