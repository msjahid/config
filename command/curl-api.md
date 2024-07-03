Token Based: curl -H "Authorization: Token 6873f30e7196f79121bdbba81171a7611daeff31" https://dushanbe-backend-apis.herokuapp.com/api/bills/

&OR:
curl https://dushanbe-backend-apis.herokuapp.com/api/bills/ -H "Authorization: Token 6873f30e7196f79121bdbba81171a7611daeff31"



Full Information: curl -i http://dushanbe-backend-apis.herokuapp.com/api/bills/ -H "Authorization: Token 6873f30e7196f79121bdbba81171a7611daeff31" 



With Auth: curl -u "admin@email.com:admin" https://dushanbe-backend-apis.herokuapp.com/api/bills/ -H "Authorization: Token 6873f30e7196f79121bdbba81171a7611daeff31"



Another way: curl -X GET https://dushanbe-backend-apis.herokuapp.com/api/bills/ -H 'Authorization: Token 6873f30e7196f79121bdbba81171a7611daeff31'

Better View: curl -X GET https://dushanbe-backend-apis.herokuapp.com/api/bills/ -H 'Authorization: Token 6873f30e7196f79121bdbba81171a7611daeff31' | fx .
