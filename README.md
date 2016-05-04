### MIGRAR JOOMLA 2.x para 3.x

```sh
Recentemente precisei migrar o contudo de um site joomla 2.5 para 3.4 que até o momento era a ultima versão.
Encontrei diversos componentes que fariam a tarefa no JED todos muito caros e pago em bolares, como eu não queria gastar nada com aquelas tarefa
Foi a luta e tentar fazer as coisas do meu jeito “HARD CODE”.

Primeira coisa que fiz foi localizar as tabelas #__content, sabendo que lá é onde fica todo os meus conteúdos no joomla (#__) significar o prefixo da tabela.
Após isso fui WORKBENCH (mysql) e separei todas as colunas que iria precisar comparando com a nova tabela do joomla 3.X ficou algo mais ou menos assim.

id,	
asset_id,		
title,				
alias,				
introtext,	
fulltext,	
state,		
catid,
created,
created_by,
created_by_alias,
modified,
modified_by,
checked_out,
checked_out_time,
publish_up,
publish_down,
images,
urls,
attribs,
version,
ordering,
metakey,
metadesc,
access,
hits,
metadata,
featured,
language,
xreference

Após saber todos os campos que eu precisaria extrair da tabela antiga eu fiz uma comparação com a nova tabela para saber os campos igual e os que eu não precisaria usar, e me sobraram esses seguintes campos.

id, asset_id, title, alias, introtext, 
	`fulltext`, state, catid, created, 
	created_by, created_by_alias, modified, 
	modified_by, checked_out, checked_out_time, 
	publish_up, publish_down, images, 
	urls, attribs, version, ordering, 
	metakey, metadesc, access, hits, metadata, 
	featured, `language`, xreference

Então eu exportei a tabela antiga para o banco novo junto com a nova tabela de conteúdos, pois assim seria mais fácil executar um INSERT com um SELECT encadeado, tipo assim: 

INSERT INTO table2
(column_name(s))
SELECT column_name(s)
FROM table1;

* Então depois das duas tabelas estarem juntas eu montei esse SCRIPT SQL que ficou assim:

INSERT INTO i6zo7_content (
	id, asset_id, title, alias, introtext, 
	`fulltext`, state, catid, created, 
	created_by, created_by_alias, modified, 
	modified_by, checked_out, checked_out_time, 
	publish_up, publish_down, images, 
	urls, attribs, version, ordering, 
	metakey, metadesc, access, hits, metadata, 
	featured, `language`, xreference
) 
SELECT 
	id, 
	asset_id, 
	title, 
	alias, 
	introtext, 
	`fulltext`, 
	state, 
	catid, 
	created, 
	created_by, 
	created_by_alias, 
	modified, 
	modified_by, 
	checked_out, 
	checked_out_time, 
	publish_up, 
	publish_down, 
	images, 
	urls, 
	attribs, 
	version, 
	ordering, 
	metakey, 
	metadesc, 
	access, 
	hits, 
	metadata, 
	featured, 
	`language`, 
	xreference 
FROM 
	jos_content

E ai TA NAN NAN =) prontinho todos os conteúdos do meu joomla 2.5 ja estava no meu Joomla 3.4 =)
Espero que essa ideia funciona para mais pessoas. e quem quiser me incentivar a fazer mais matérias como essa da uma força no linkedin e canal do youtube…


