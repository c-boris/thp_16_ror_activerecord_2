rails generate model Album title:string artist:string

rails generate model Track title:string album:string artist:string duration:integer size:integer price:float

rails db:migrate

rails db:seed

Pour trouver le nombre total d'objets Album dans la base de données :
Album.count

Pour trouver l'auteur de la chanson "White Room" :
Track.find_by(title: "White Room").artist

Pour trouver la chanson qui dure exactement 188133 millisecondes :
Track.find_by(duration: 188133).title

Pour trouver le groupe qui a sorti l'album "Use Your Illusion II" :
Album.find_by(title: "Use Your Illusion II").artist

Pour trouver le nombre d'albums dont le titre contient "Great" :
Album.where("title LIKE ?", "%Great%").count

Pour supprimer tous les albums dont le nom contient "music" :
Album.where("title LIKE ?", "%music%").destroy_all

Pour trouver le nombre de chansons écrites par AC/DC :
Track.where(artist: "AC/DC").count

Pour trouver le nombre de chansons qui durent exactement 158589 millisecondes:
Track.where(duration: 158589).count

Pour afficher tous les titres de AC/DC :
Track.where(artist: "AC/DC").pluck(:title)

Pour afficher tous les titres de l'album "Let There Be Rock" :
Track.where(album: "Let There Be Rock").pluck(:title)

Pour calculer le prix total et la durée totale de l'album "Let There Be Rock" :
let_there_be_rock = Album.find_by(title: "Let There Be Rock")
total_price = Track.where(album: let_there_be_rock).sum(:price)
total_duration = Track.where(album: let_there_be_rock).sum(:duration)
puts "Le prix total de l'album est de #{total_price} dollars et sa durée totale est de #{total_duration} millisecondes."

Pour calculer le coût de l'intégralité de la discographie de "Deep Purple" :
deep_purple_tracks = Track.where(artist: "Deep Purple")
total_cost = deep_purple_tracks.sum(:price) * deep_purple_tracks.count
puts "Le coût de l'intégralité de la discographie de Deep Purple est de #{total_cost} dollars."

Pour modifier tous les titres de "Eric Clapton" pour qu'ils soient affichés avec "Britney Spears" en tant qu'artiste :
Track.where(artist: "Eric Clapton").each do |track|
  track.update(artist: "Britney Spears", title: "Britney Spears - #{track.title}")
end