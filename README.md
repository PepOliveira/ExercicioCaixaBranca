# ExercicioOhata
Etapas com Perguntas e Respostas

Etapa 1 – Caixa Branca
Aponte os erros que podem conter no código;
Respostas:
•	a string "com.mysql.Driver.Manager" não está formatada corretamente porque segundo as pesquisas feitas o nome correto do driver MySQL é "com.mysql.cj.jdbc.Driver".
•	a prática recomendada por "segurança" é separar o nome de usuário e a senha usando métodos da API de conexão, não concatenar na URL, pois possivelmente assim poderia “vazar” dados de quem está comandando a API 
•	se a conexão falhar no bloco try na linha ""return conn;"", o método ainda retornará null, o que causará erros durante a rodagem do código.
•	quando concatenamos strings diretamente em códigos SQL isso pode virar uma prática insegura que deixa o código vulnerável a ataques de SQL Injection. Podemos usar o "PreparedStatement" para evitar esse problema, como por exemplo:
String sql = "SELECT nome FROM usuarios WHERE login = ? AND senha = ?";
PreparedStatement pst = conn.prepareStatement(sql);
pst.setString(1, login);
pst.setString(2, senha);
ResultSet rs = pst.executeQuery();
•	quando usamos o ""catch"", poderiamos deixar mais explicito o que a Exception queria "puxar" para o código na linha
•	os recursos como Statement e ResultSet não são fechados, o que pode causar vazamentos de memória. Podemos usar ""try-with-resources"" para garantir que esses recursos sejam fechados automaticamente

Perguntas do Slide:

• Documentação foi descrita o Código?
não, o código não contém comentários que expliquem o código, o que podemos ver de comentário é sobre o inicio das instruções SQL. Mas não é de dificil entendimento saber do que se trata o código
• As variáveis e constantes possuem boa nomenclatura?
elas possuem um nomenclatura relativamente boa, mas estão abreviadas e isso pode fazer com que alguém menos experiente possa se perder para entender o código. Podemos notar as abreviações em: “conn” para connection e “st” para statement.
• Existe legibilidade e organização no código?
sim, mas poderia melhorar, como por exemplo se caso o usuário colocasse alguma credencial errada, o sistema poderia emitir uma mensagem de erro, um “pop-up” por exemplo. Seria uma alternativa mais "segura" de alertar o usuario sobre um erro de credenciais
• Todos os nullpoints foram tratados?
não, se caso o “conn” fosse “null” em formato booleano, nós poderíamos ver um nullpointer com a falha do banco de dados.
se caso o “rs.next” onde o “rs” for “null” nós poderiamos presenciar um nullpointer.
• A arquitetura usada foi devidamente respeitada?
o banco de dados poderia ser fechado para mais segurança e evitar possiveis "invasões"
o SQL poderia sofrer ataques com facilidade por ser “ simples”, poderíamos usar “statement” para uma melhor segurança.
• As conexões foram fechadas?
não, isso pode causar um vazamento de dados dos usuários pois temos conexões em aberto como “ResultSet” ; “Statement” e “Connection”.

Código comentado (cada número com  um "*" é um Nó)

import java.sql.Connection; 
import java.sql.DriverManager; 
import java.sql.ResultSet; 
import java.sql.Statement;
1* public class User {
1* public Connection conectarBD() {
2*   Connection conn = null; 
3*   try { 
Class.forName("com.mysql.jdbc.Driver").newInstance(); 
String url = "jdbc: mysql://127.0.0.1/test?user=lopes&password=123"; conn = DriverManager.getConnection(url); 
4*   } catch (Exception e) {
   } 
5*   return conn; 
    }
    public String nome = "";
    public boolean result = false;
6* public boolean verificarUsuario(String login, String senha) {
7*   String sql = ""; 
8*   Connection conn = conectarBD(); 
//INSTRUÇÃO SQL 
9*    sql += "select nome from usuarios"; 
9*    sql += "where login = '" + login + "'";
9*    sql += "and senha = '" + senha + "'"; 
10*    try { 
Statement st = conn.createStatement(); 
ResultSet rs = st.executeQuery(sql); 
11*    if (rs.next()) { 
result = true; 
nome = rs.getString("nome"); } 
12*   } catch (Exception e) { } 
13*   return result; } }



PLANILHA CAIXA BRANCA RESPONDIDA CONFORME AS PERGUNTAS:
[PLANO DE TESTE-1-1 (1).xlsx](https://github.com/user-attachments/files/17804238/PLANO.DE.TESTE-1-1.1.xlsx)

