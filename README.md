# ScriptRDiabetes
Scripts que se ejecutan sobre software R usando un set de datos de diabetes
library(mongolite)

connection_string = 'mongodb+"aqui va la url de mongodb"/CancerDB'

Coleccion = mongo(collection="DiabetesCollection", db="DiabetesDB", url=connection_string)

Coleccion$count()

Datos.Diabetes = Coleccion$find()
