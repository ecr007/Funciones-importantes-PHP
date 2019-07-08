# Funciones-importantes-PHP


<div class="classic"><blockquote><div class="citacuerpo"><a href="/lanota"><img src="https://r.kn3.net/taringa_defaults/avatares/m/16x16_3.jpg"></a><a href="/lanota">lanota</a> dijo:Post editado y mejorado para la version 5 de Taringa. Los usuarios con la version 5 se preguntaran, ¿pero que tiene de especial? , la simplicidad hace juego en la v5 </div></blockquote>
<br>
<br><span style="font-family:Arial">Tener el script correcto en el momento adecuado puede ser un salvavidas para muchos desarrolladores. Hoy he compilado 10 scripts que espero puedan ser utiles en su evolucion como desarrolladores web.</span>
<br>
<br><strong><span style="font-size:18pt; line-height:18pt">Simple Sistema de Almacenamiento de Caché</span></strong>
<br>
<br><span style="font-family:Arial">Cuando tu proyecto web no esta basado en un CMS o en un framework, puede ser una buena idea implementar un sistema de almacenamiento de caché en tus paginas. El codigo es muy simple pero sirve para webs pequeñas.</span>
<br>
<br><code><span style="color:#000000">

<br><span style="color:#0000BB">&lt;?php
<br>&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#FF8000">//&nbsp;Define&nbsp;la&nbsp;ruta&nbsp;y&nbsp;nombre&nbsp;del&nbsp;archivo&nbsp;que&nbsp;se&nbsp;almacenara&nbsp;el&nbsp;cache
<br>&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">$cachefile&nbsp;</span><span style="color:#007700">=&nbsp;</span><span style="color:#DD0000">'cached-files/'</span><span style="color:#007700">.</span><span style="color:#0000BB">date</span><span style="color:#007700">(</span><span style="color:#DD0000">'M-d-Y'</span><span style="color:#007700">).</span><span style="color:#DD0000">'.php'</span><span style="color:#007700">;
<br>&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#FF8000">//&nbsp;define&nbsp;el&nbsp;tiempo&nbsp;que&nbsp;queremos&nbsp;esperar&nbsp;el&nbsp;archivo&nbsp;en&nbsp;segundos.Yo&nbsp;puse&nbsp;el&nbsp;mio&nbsp;en&nbsp;5&nbsp;horas.
<br>&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">$cachetime&nbsp;</span><span style="color:#007700">=&nbsp;</span><span style="color:#0000BB">18000</span><span style="color:#007700">;
<br>&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#FF8000">//&nbsp;Revisa&nbsp;si&nbsp;el&nbsp;cache&nbsp;sigue&nbsp;fresco&nbsp;(activo).&nbsp;En&nbsp;el&nbsp;caso&nbsp;de&nbsp;que&nbsp;si&nbsp;lo&nbsp;incluye&nbsp;y&nbsp;sale
<br>&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#007700">if&nbsp;(</span><span style="color:#0000BB">file_exists</span><span style="color:#007700">(</span><span style="color:#0000BB">$cachefile</span><span style="color:#007700">)&nbsp;&amp;&amp;&nbsp;</span><span style="color:#0000BB">time</span><span style="color:#007700">()&nbsp;-&nbsp;</span><span style="color:#0000BB">$cachetime&nbsp;</span><span style="color:#007700">&lt;&nbsp;</span><span style="color:#0000BB">filemtime</span><span style="color:#007700">(</span><span style="color:#0000BB">$cachefile</span><span style="color:#007700">))&nbsp;{
<br>&nbsp;&nbsp;&nbsp;&nbsp;include(</span><span style="color:#0000BB">$cachefile</span><span style="color:#007700">);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;exit;
<br>&nbsp;&nbsp;&nbsp;&nbsp;}
<br>&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#FF8000">//&nbsp;Si&nbsp;no&nbsp;hay&nbsp;archivo&nbsp;o&nbsp;es&nbsp;demasiado&nbsp;viejo.&nbsp;Renderiza&nbsp;la&nbsp;pagina&nbsp;y&nbsp;muestra&nbsp;el&nbsp;HTML
<br>&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">ob_start</span><span style="color:#007700">();
<br></span><span style="color:#0000BB">?&gt;
<br></span>&nbsp;&nbsp;&nbsp;&nbsp;&lt;html&gt;
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;todo&nbsp;tu&nbsp;html&nbsp;aca
<br>&nbsp;&nbsp;&nbsp;&nbsp;&lt;/html&gt;
<br><span style="color:#0000BB">&lt;?php
<br>&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#FF8000">//&nbsp;Listo!.&nbsp;Guardamos&nbsp;el&nbsp;cache&nbsp;en&nbsp;un&nbsp;archivo
<br>&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">$fp&nbsp;</span><span style="color:#007700">=&nbsp;</span><span style="color:#0000BB">fopen</span><span style="color:#007700">(</span><span style="color:#0000BB">$cachefile</span><span style="color:#007700">,&nbsp;</span><span style="color:#DD0000">'w'</span><span style="color:#007700">);
<br>&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">fwrite</span><span style="color:#007700">(</span><span style="color:#0000BB">$fp</span><span style="color:#007700">,&nbsp;</span><span style="color:#0000BB">ob_get_contents</span><span style="color:#007700">());
<br>&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">fclose</span><span style="color:#007700">(</span><span style="color:#0000BB">$fp</span><span style="color:#007700">);
<br>&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#FF8000">//&nbsp;finalmente&nbsp;se&nbsp;lo&nbsp;enviamos&nbsp;al&nbsp;navegador
<br>&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">ob_end_flush</span><span style="color:#007700">();
<br></span><span style="color:#0000BB">?&gt;
<br></span>
</span>
</code>
<br>
<br><strong><span style="font-size:18pt; line-height:18pt">Calcula Distancias en PHP</span></strong>
<br>
<br><span style="font-family:Arial">Aqui hay una funcion muy util que calcula distancias de un punto A a un punto B usando latitudes y longitudes. La funcion puede regresar distancias en millas, kilometros o millas nauticas</span>
<br>
<br>
<br><code><span style="color:#000000">

<br><span style="color:#0000BB">&lt;?
<br></span><span style="color:#007700">function&nbsp;</span><span style="color:#0000BB">distance</span><span style="color:#007700">(</span><span style="color:#0000BB">$lat1</span><span style="color:#007700">,&nbsp;</span><span style="color:#0000BB">$lon1</span><span style="color:#007700">,&nbsp;</span><span style="color:#0000BB">$lat2</span><span style="color:#007700">,&nbsp;</span><span style="color:#0000BB">$lon2</span><span style="color:#007700">,&nbsp;</span><span style="color:#0000BB">$unit</span><span style="color:#007700">)&nbsp;{&nbsp;
<br>
<br>&nbsp;&nbsp;</span><span style="color:#0000BB">$theta&nbsp;</span><span style="color:#007700">=&nbsp;</span><span style="color:#0000BB">$lon1&nbsp;</span><span style="color:#007700">-&nbsp;</span><span style="color:#0000BB">$lon2</span><span style="color:#007700">;
<br>&nbsp;&nbsp;</span><span style="color:#0000BB">$dist&nbsp;</span><span style="color:#007700">=&nbsp;</span><span style="color:#0000BB">sin</span><span style="color:#007700">(</span><span style="color:#0000BB">deg2rad</span><span style="color:#007700">(</span><span style="color:#0000BB">$lat1</span><span style="color:#007700">))&nbsp;*&nbsp;</span><span style="color:#0000BB">sin</span><span style="color:#007700">(</span><span style="color:#0000BB">deg2rad</span><span style="color:#007700">(</span><span style="color:#0000BB">$lat2</span><span style="color:#007700">))&nbsp;+&nbsp;&nbsp;</span><span style="color:#0000BB">cos</span><span style="color:#007700">(</span><span style="color:#0000BB">deg2rad</span><span style="color:#007700">(</span><span style="color:#0000BB">$lat1</span><span style="color:#007700">))&nbsp;*&nbsp;</span><span style="color:#0000BB">cos</span><span style="color:#007700">(</span><span style="color:#0000BB">deg2rad</span><span style="color:#007700">(</span><span style="color:#0000BB">$lat2</span><span style="color:#007700">))&nbsp;*&nbsp;</span><span style="color:#0000BB">cos</span><span style="color:#007700">(</span><span style="color:#0000BB">deg2rad</span><span style="color:#007700">(</span><span style="color:#0000BB">$theta</span><span style="color:#007700">));
<br>&nbsp;&nbsp;</span><span style="color:#0000BB">$dist&nbsp;</span><span style="color:#007700">=&nbsp;</span><span style="color:#0000BB">acos</span><span style="color:#007700">(</span><span style="color:#0000BB">$dist</span><span style="color:#007700">);
<br>&nbsp;&nbsp;</span><span style="color:#0000BB">$dist&nbsp;</span><span style="color:#007700">=&nbsp;</span><span style="color:#0000BB">rad2deg</span><span style="color:#007700">(</span><span style="color:#0000BB">$dist</span><span style="color:#007700">);
<br>&nbsp;&nbsp;</span><span style="color:#0000BB">$miles&nbsp;</span><span style="color:#007700">=&nbsp;</span><span style="color:#0000BB">$dist&nbsp;</span><span style="color:#007700">*&nbsp;</span><span style="color:#0000BB">60&nbsp;</span><span style="color:#007700">*&nbsp;</span><span style="color:#0000BB">1.1515</span><span style="color:#007700">;
<br>&nbsp;&nbsp;</span><span style="color:#0000BB">$unit&nbsp;</span><span style="color:#007700">=&nbsp;</span><span style="color:#0000BB">strtoupper</span><span style="color:#007700">(</span><span style="color:#0000BB">$unit</span><span style="color:#007700">);
<br>
<br>&nbsp;&nbsp;if&nbsp;(</span><span style="color:#0000BB">$unit&nbsp;</span><span style="color:#007700">==&nbsp;</span><span style="color:#DD0000">"K"</span><span style="color:#007700">)&nbsp;{
<br>&nbsp;&nbsp;&nbsp;&nbsp;return&nbsp;(</span><span style="color:#0000BB">$miles&nbsp;</span><span style="color:#007700">*&nbsp;</span><span style="color:#0000BB">1.609344</span><span style="color:#007700">);
<br>&nbsp;&nbsp;}&nbsp;else&nbsp;if&nbsp;(</span><span style="color:#0000BB">$unit&nbsp;</span><span style="color:#007700">==&nbsp;</span><span style="color:#DD0000">"N"</span><span style="color:#007700">)&nbsp;{
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return&nbsp;(</span><span style="color:#0000BB">$miles&nbsp;</span><span style="color:#007700">*&nbsp;</span><span style="color:#0000BB">0.8684</span><span style="color:#007700">);
<br>&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;else&nbsp;{
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return&nbsp;</span><span style="color:#0000BB">$miles</span><span style="color:#007700">;
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}
<br>}
<br></span><span style="color:#0000BB">?&gt;
<br></span>
</span>
</code>
<br>
<br>Forma de uso
<br>
<br><code><span style="color:#000000">
&nbsp;<span style="color:#0000BB">&lt;?&nbsp;</span><span style="color:#007700">echo&nbsp;</span><span style="color:#0000BB">distance</span><span style="color:#007700">(</span><span style="color:#0000BB">32.9697</span><span style="color:#007700">,&nbsp;-</span><span style="color:#0000BB">96.80322</span><span style="color:#007700">,&nbsp;</span><span style="color:#0000BB">29.46786</span><span style="color:#007700">,&nbsp;-</span><span style="color:#0000BB">98.53506</span><span style="color:#007700">,&nbsp;</span><span style="color:#DD0000">"k"</span><span style="color:#007700">).</span><span style="color:#DD0000">"&nbsp;kilometros"</span><span style="color:#007700">;&nbsp;</span><span style="color:#0000BB">?&gt;</span>
</span>
</code>
<br>
<br><a href="http://www.phpsnippets.info/calculate-distances-in-php" rel="nofollow" target="_blank">Fuente</a>
<br>
<br>
<br><strong><span style="font-size:18pt; line-height:18pt">Convierte segundos a tiempo (años,meses,dias,horas...)</span></strong>
<br>
<br><span style="font-family:Arial">Util funcion que convertira segundos facilmente en años,meses,dias,horas y etc.</span>
<br>
<br><code><span style="color:#000000">

<br><span style="color:#0000BB">&lt;?php
<br>
<br>
<br></span><span style="color:#007700">function&nbsp;</span><span style="color:#0000BB">Sec2Time</span><span style="color:#007700">(</span><span style="color:#0000BB">$time</span><span style="color:#007700">){
<br>&nbsp;&nbsp;if(</span><span style="color:#0000BB">is_numeric</span><span style="color:#007700">(</span><span style="color:#0000BB">$time</span><span style="color:#007700">)){
<br>&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">$value&nbsp;</span><span style="color:#007700">=&nbsp;array(
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#DD0000">"years"&nbsp;</span><span style="color:#007700">=&gt;&nbsp;</span><span style="color:#0000BB">0</span><span style="color:#007700">,&nbsp;</span><span style="color:#DD0000">"days"&nbsp;</span><span style="color:#007700">=&gt;&nbsp;</span><span style="color:#0000BB">0</span><span style="color:#007700">,&nbsp;</span><span style="color:#DD0000">"hours"&nbsp;</span><span style="color:#007700">=&gt;&nbsp;</span><span style="color:#0000BB">0</span><span style="color:#007700">,
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#DD0000">"minutes"&nbsp;</span><span style="color:#007700">=&gt;&nbsp;</span><span style="color:#0000BB">0</span><span style="color:#007700">,&nbsp;</span><span style="color:#DD0000">"seconds"&nbsp;</span><span style="color:#007700">=&gt;&nbsp;</span><span style="color:#0000BB">0</span><span style="color:#007700">,
<br>&nbsp;&nbsp;&nbsp;&nbsp;);
<br>&nbsp;&nbsp;&nbsp;&nbsp;if(</span><span style="color:#0000BB">$time&nbsp;</span><span style="color:#007700">&gt;=&nbsp;</span><span style="color:#0000BB">31556926</span><span style="color:#007700">){
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">$value</span><span style="color:#007700">[</span><span style="color:#DD0000">"years"</span><span style="color:#007700">]&nbsp;=&nbsp;</span><span style="color:#0000BB">floor</span><span style="color:#007700">(</span><span style="color:#0000BB">$time</span><span style="color:#007700">/</span><span style="color:#0000BB">31556926</span><span style="color:#007700">);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">$time&nbsp;</span><span style="color:#007700">=&nbsp;(</span><span style="color:#0000BB">$time</span><span style="color:#007700">%</span><span style="color:#0000BB">31556926</span><span style="color:#007700">);
<br>&nbsp;&nbsp;&nbsp;&nbsp;}
<br>&nbsp;&nbsp;&nbsp;&nbsp;if(</span><span style="color:#0000BB">$time&nbsp;</span><span style="color:#007700">&gt;=&nbsp;</span><span style="color:#0000BB">86400</span><span style="color:#007700">){
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">$value</span><span style="color:#007700">[</span><span style="color:#DD0000">"days"</span><span style="color:#007700">]&nbsp;=&nbsp;</span><span style="color:#0000BB">floor</span><span style="color:#007700">(</span><span style="color:#0000BB">$time</span><span style="color:#007700">/</span><span style="color:#0000BB">86400</span><span style="color:#007700">);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">$time&nbsp;</span><span style="color:#007700">=&nbsp;(</span><span style="color:#0000BB">$time</span><span style="color:#007700">%</span><span style="color:#0000BB">86400</span><span style="color:#007700">);
<br>&nbsp;&nbsp;&nbsp;&nbsp;}
<br>&nbsp;&nbsp;&nbsp;&nbsp;if(</span><span style="color:#0000BB">$time&nbsp;</span><span style="color:#007700">&gt;=&nbsp;</span><span style="color:#0000BB">3600</span><span style="color:#007700">){
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">$value</span><span style="color:#007700">[</span><span style="color:#DD0000">"hours"</span><span style="color:#007700">]&nbsp;=&nbsp;</span><span style="color:#0000BB">floor</span><span style="color:#007700">(</span><span style="color:#0000BB">$time</span><span style="color:#007700">/</span><span style="color:#0000BB">3600</span><span style="color:#007700">);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">$time&nbsp;</span><span style="color:#007700">=&nbsp;(</span><span style="color:#0000BB">$time</span><span style="color:#007700">%</span><span style="color:#0000BB">3600</span><span style="color:#007700">);
<br>&nbsp;&nbsp;&nbsp;&nbsp;}
<br>&nbsp;&nbsp;&nbsp;&nbsp;if(</span><span style="color:#0000BB">$time&nbsp;</span><span style="color:#007700">&gt;=&nbsp;</span><span style="color:#0000BB">60</span><span style="color:#007700">){
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">$value</span><span style="color:#007700">[</span><span style="color:#DD0000">"minutes"</span><span style="color:#007700">]&nbsp;=&nbsp;</span><span style="color:#0000BB">floor</span><span style="color:#007700">(</span><span style="color:#0000BB">$time</span><span style="color:#007700">/</span><span style="color:#0000BB">60</span><span style="color:#007700">);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">$time&nbsp;</span><span style="color:#007700">=&nbsp;(</span><span style="color:#0000BB">$time</span><span style="color:#007700">%</span><span style="color:#0000BB">60</span><span style="color:#007700">);
<br>&nbsp;&nbsp;&nbsp;&nbsp;}
<br>&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">$value</span><span style="color:#007700">[</span><span style="color:#DD0000">"seconds"</span><span style="color:#007700">]&nbsp;=&nbsp;</span><span style="color:#0000BB">floor</span><span style="color:#007700">(</span><span style="color:#0000BB">$time</span><span style="color:#007700">);
<br>&nbsp;&nbsp;&nbsp;&nbsp;return&nbsp;(array)&nbsp;</span><span style="color:#0000BB">$value</span><span style="color:#007700">;
<br>&nbsp;&nbsp;}else{
<br>&nbsp;&nbsp;&nbsp;&nbsp;return&nbsp;(bool)&nbsp;</span><span style="color:#0000BB">FALSE</span><span style="color:#007700">;
<br>&nbsp;&nbsp;}
<br>}
<br>
<br></span><span style="color:#0000BB">?&gt;
<br></span>
<br></span>
</code>
<br><a href="http://ckorp.net/sec2time.php" rel="nofollow" target="_blank">Fuente</a>
<br>
<br>
<br><strong><span style="font-size:18pt; line-height:18pt">Forzar un archivo a descargar</span></strong>
<br>
<br><span style="font-family:Arial">Muchos formatos como el mp3, se reproducen directamente a traves del navegador, pero si prefieres que sean descargados directamente, el siguiente script te facilitara mucho el trabajo</span>
<br>
<br><code><span style="color:#000000">

<br><span style="color:#0000BB">&lt;?
<br></span><span style="color:#007700">function&nbsp;</span><span style="color:#0000BB">downloadFile</span><span style="color:#007700">(</span><span style="color:#0000BB">$file</span><span style="color:#007700">){
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">$file_name&nbsp;</span><span style="color:#007700">=&nbsp;</span><span style="color:#0000BB">$file</span><span style="color:#007700">;
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">$mime&nbsp;</span><span style="color:#007700">=&nbsp;</span><span style="color:#DD0000">'application/force-download'</span><span style="color:#007700">;
<br>&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">header</span><span style="color:#007700">(</span><span style="color:#DD0000">'Pragma:&nbsp;public'</span><span style="color:#007700">);&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#FF8000">//&nbsp;required
<br>&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">header</span><span style="color:#007700">(</span><span style="color:#DD0000">'Expires:&nbsp;0'</span><span style="color:#007700">);&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#FF8000">//&nbsp;no&nbsp;cache
<br>&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">header</span><span style="color:#007700">(</span><span style="color:#DD0000">'Cache-Control:&nbsp;must-revalidate,&nbsp;post-check=0,&nbsp;pre-check=0'</span><span style="color:#007700">);
<br>&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">header</span><span style="color:#007700">(</span><span style="color:#DD0000">'Cache-Control:&nbsp;private'</span><span style="color:#007700">,</span><span style="color:#0000BB">false</span><span style="color:#007700">);
<br>&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">header</span><span style="color:#007700">(</span><span style="color:#DD0000">'Content-Type:&nbsp;'</span><span style="color:#007700">.</span><span style="color:#0000BB">$mime</span><span style="color:#007700">);
<br>&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">header</span><span style="color:#007700">(</span><span style="color:#DD0000">'Content-Disposition:&nbsp;attachment;&nbsp;filename="'</span><span style="color:#007700">.</span><span style="color:#0000BB">basename</span><span style="color:#007700">(</span><span style="color:#0000BB">$file_name</span><span style="color:#007700">).</span><span style="color:#DD0000">'"'</span><span style="color:#007700">);
<br>&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">header</span><span style="color:#007700">(</span><span style="color:#DD0000">'Content-Transfer-Encoding:&nbsp;binary'</span><span style="color:#007700">);
<br>&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">header</span><span style="color:#007700">(</span><span style="color:#DD0000">'Connection:&nbsp;close'</span><span style="color:#007700">);
<br>&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">readfile</span><span style="color:#007700">(</span><span style="color:#0000BB">$file_name</span><span style="color:#007700">);&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#FF8000">//&nbsp;push&nbsp;it&nbsp;out
<br>&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#007700">exit();
<br>}
<br></span><span style="color:#0000BB">?&gt;
<br></span>
</span>
</code>
<br>
<br><a href="http://www.tecnocrazia.com/" rel="nofollow" target="_blank">Fuente</a>
<br>
<br>
<br><strong><span style="font-size:18pt; line-height:18pt">Obtener el clima actual con el API de google</span></strong>
<br>
<br><span style="font-family:Arial">Quieres saber el clima de hoy? Este script te lo hara saber, en tan solo 3 lineas de codigo, lo unico que tienes que hacer es cambiar DIRECCION por la direccion deseada</span>
<br>
<br><code><span style="color:#000000">

<br><span style="color:#0000BB">&lt;?
<br>$xml&nbsp;</span><span style="color:#007700">=&nbsp;</span><span style="color:#0000BB">simplexml_load_file</span><span style="color:#007700">(</span><span style="color:#DD0000">'http://www.google.com/ig/api?weather=DIRECCION'</span><span style="color:#007700">);
<br>&nbsp;&nbsp;</span><span style="color:#0000BB">$information&nbsp;</span><span style="color:#007700">=&nbsp;</span><span style="color:#0000BB">$xml</span><span style="color:#007700">-&gt;</span><span style="color:#0000BB">xpath</span><span style="color:#007700">(</span><span style="color:#DD0000">"/xml_api_reply/weather/current_conditions/condition"</span><span style="color:#007700">);
<br>&nbsp;&nbsp;echo&nbsp;</span><span style="color:#0000BB">$information</span><span style="color:#007700">[</span><span style="color:#0000BB">0</span><span style="color:#007700">]-&gt;</span><span style="color:#0000BB">attributes</span><span style="color:#007700">();
<br></span><span style="color:#0000BB">?&gt;
<br></span>
</span>
</code>
<br>
<br><a href="http://ortanotes.tumblr.com/post/200469319/current-weather-in-3-lines-of-php" rel="nofollow" target="_blank">Fuente</a>
<br>
<br>
<br>
<br><strong><span style="font-size:18pt; line-height:18pt">whois basico con PHP</span></strong>
<br>
<br><span style="font-family:Arial">Whois es un servicio muy util para saber informacion basica acerca de un dominio: nombre del propietario,fecha de creacion, etc. Usando php y el comando whois de unix es muy facil hacer un script basico de whois en PHP. Por favor note que el comando whois debe estar instalado en el servidor antes de usarlo</span>
<br>
<br><code><span style="color:#000000">

<br><span style="color:#0000BB">&lt;?
<br>$domains&nbsp;</span><span style="color:#007700">=&nbsp;array(</span><span style="color:#DD0000">'home.pl'</span><span style="color:#007700">,&nbsp;</span><span style="color:#DD0000">'w3c.org'</span><span style="color:#007700">);
<br>
<br>function&nbsp;</span><span style="color:#0000BB">creation_date</span><span style="color:#007700">(</span><span style="color:#0000BB">$domain</span><span style="color:#007700">)&nbsp;{
<br>&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">$lines&nbsp;</span><span style="color:#007700">=&nbsp;</span><span style="color:#0000BB">explode</span><span style="color:#007700">(</span><span style="color:#DD0000">"n"</span><span style="color:#007700">,&nbsp;`</span><span style="color:#DD0000">whois&nbsp;</span><span style="color:#0000BB">$domain</span><span style="color:#007700">`);
<br>&nbsp;&nbsp;&nbsp;&nbsp;foreach(</span><span style="color:#0000BB">$lines&nbsp;</span><span style="color:#007700">as&nbsp;</span><span style="color:#0000BB">$line</span><span style="color:#007700">)&nbsp;{
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;if(</span><span style="color:#0000BB">strpos</span><span style="color:#007700">(</span><span style="color:#0000BB">strtolower</span><span style="color:#007700">(</span><span style="color:#0000BB">$line</span><span style="color:#007700">),&nbsp;</span><span style="color:#DD0000">'created'</span><span style="color:#007700">)&nbsp;!==&nbsp;</span><span style="color:#0000BB">false</span><span style="color:#007700">)&nbsp;{
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return&nbsp;</span><span style="color:#0000BB">$line</span><span style="color:#007700">;
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}
<br>&nbsp;&nbsp;&nbsp;&nbsp;}
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;return&nbsp;</span><span style="color:#0000BB">false</span><span style="color:#007700">;
<br>}
<br>
<br>foreach(</span><span style="color:#0000BB">$domains&nbsp;</span><span style="color:#007700">as&nbsp;</span><span style="color:#0000BB">$d</span><span style="color:#007700">)&nbsp;{
<br>&nbsp;&nbsp;&nbsp;&nbsp;echo&nbsp;</span><span style="color:#0000BB">creation_date</span><span style="color:#007700">(</span><span style="color:#0000BB">$d</span><span style="color:#007700">)&nbsp;.&nbsp;</span><span style="color:#DD0000">"n"</span><span style="color:#007700">;
<br>}
<br>
<br></span><span style="color:#0000BB">?&gt;
<br></span>
</span>
</code>
<br><a href="http://snipplr.com/view.php?codeview&amp;id=48040" rel="nofollow" target="_blank">Fuente</a>
<br>
<br>
<br><strong><span style="font-size:18pt; line-height:18pt">Obtener Latitud y Longitud de Una Direccion</span></strong>
<br>
<br><span style="font-family:Arial">
<br>Con la popularidad del API de google maps,los desarrolladores a menudo necesitaran saber sobre la longitud y latitud de determinado lugar. Esta util funcion tomara una direccion como parametro y devolvera en un array ambos datos: Longitud y latitud.</span>
<br>
<br><code><span style="color:#000000">

<br><span style="color:#0000BB">&lt;?
<br></span><span style="color:#007700">function&nbsp;</span><span style="color:#0000BB">getLatLong</span><span style="color:#007700">(</span><span style="color:#0000BB">$address</span><span style="color:#007700">){
<br>&nbsp;&nbsp;&nbsp;&nbsp;if&nbsp;(!</span><span style="color:#0000BB">is_string</span><span style="color:#007700">(</span><span style="color:#0000BB">$address</span><span style="color:#007700">))die(</span><span style="color:#DD0000">"Todas&nbsp;las&nbsp;direcciones&nbsp;se&nbsp;validaran&nbsp;como&nbsp;srtings"</span><span style="color:#007700">);
<br>&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">$_url&nbsp;</span><span style="color:#007700">=&nbsp;</span><span style="color:#0000BB">sprintf</span><span style="color:#007700">(</span><span style="color:#DD0000">'http://maps.google.com/maps?output=js&amp;q=%s'</span><span style="color:#007700">,</span><span style="color:#0000BB">rawurlencode</span><span style="color:#007700">(</span><span style="color:#0000BB">$address</span><span style="color:#007700">));
<br>&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">$_result&nbsp;</span><span style="color:#007700">=&nbsp;</span><span style="color:#0000BB">false</span><span style="color:#007700">;
<br>&nbsp;&nbsp;&nbsp;&nbsp;if(</span><span style="color:#0000BB">$_result&nbsp;</span><span style="color:#007700">=&nbsp;</span><span style="color:#0000BB">file_get_contents</span><span style="color:#007700">(</span><span style="color:#0000BB">$_url</span><span style="color:#007700">))&nbsp;{
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;if(</span><span style="color:#0000BB">strpos</span><span style="color:#007700">(</span><span style="color:#0000BB">$_result</span><span style="color:#007700">,</span><span style="color:#DD0000">'errortips'</span><span style="color:#007700">)&nbsp;&gt;&nbsp;</span><span style="color:#0000BB">1&nbsp;</span><span style="color:#007700">||&nbsp;</span><span style="color:#0000BB">strpos</span><span style="color:#007700">(</span><span style="color:#0000BB">$_result</span><span style="color:#007700">,</span><span style="color:#DD0000">'Did&nbsp;you&nbsp;mean:'</span><span style="color:#007700">)&nbsp;!==&nbsp;</span><span style="color:#0000BB">false</span><span style="color:#007700">)&nbsp;return&nbsp;</span><span style="color:#0000BB">false</span><span style="color:#007700">;
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">preg_match</span><span style="color:#007700">(</span><span style="color:#DD0000">'!center:s*{lat:s*(-?d+.d+),lng:s*(-?d+.d+)}!U'</span><span style="color:#007700">,&nbsp;</span><span style="color:#0000BB">$_result</span><span style="color:#007700">,&nbsp;</span><span style="color:#0000BB">$_match</span><span style="color:#007700">);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">$_coords</span><span style="color:#007700">[</span><span style="color:#DD0000">'lat'</span><span style="color:#007700">]&nbsp;=&nbsp;</span><span style="color:#0000BB">$_match</span><span style="color:#007700">[</span><span style="color:#0000BB">1</span><span style="color:#007700">];
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">$_coords</span><span style="color:#007700">[</span><span style="color:#DD0000">'long'</span><span style="color:#007700">]&nbsp;=&nbsp;</span><span style="color:#0000BB">$_match</span><span style="color:#007700">[</span><span style="color:#0000BB">2</span><span style="color:#007700">];
<br>&nbsp;&nbsp;&nbsp;&nbsp;}
<br>&nbsp;&nbsp;&nbsp;&nbsp;return&nbsp;</span><span style="color:#0000BB">$_coords</span><span style="color:#007700">;
<br>}
<br>
<br></span><span style="color:#0000BB">?&gt;
<br></span>
</span>
</code>
<br>
<br><a href="http://snipplr.com/view.php?codeview&amp;id=47806" rel="nofollow" target="_blank">Fuente</a>
<br>
<br><strong>
<br><span style="font-size:18pt; line-height:18pt">Obtener el dominio del FavIcon usando PHP y Google</span></strong>
<br>
<br><span style="font-family:Arial">
<br>En estos dias muchos websites o WebApps estan robando favicons de otras webs. Mostrar un favicon en tu sitio es muy facil con php y ayuda de Google</span>
<br>
<br><code><span style="color:#000000">

<br><span style="color:#0000BB">&lt;?
<br></span><span style="color:#007700">function&nbsp;</span><span style="color:#0000BB">get_favicon</span><span style="color:#007700">(</span><span style="color:#0000BB">$url</span><span style="color:#007700">){
<br>&nbsp;&nbsp;</span><span style="color:#0000BB">$url&nbsp;</span><span style="color:#007700">=&nbsp;</span><span style="color:#0000BB">str_replace</span><span style="color:#007700">(</span><span style="color:#DD0000">"http://"</span><span style="color:#007700">,</span><span style="color:#DD0000">''</span><span style="color:#007700">,</span><span style="color:#0000BB">$url</span><span style="color:#007700">);
<br>&nbsp;&nbsp;return&nbsp;</span><span style="color:#DD0000">"http://www.google.com/s2/favicons?domain="</span><span style="color:#007700">.</span><span style="color:#0000BB">$url</span><span style="color:#007700">;
<br>}
<br></span><span style="color:#0000BB">?&gt;
<br></span>
</span>
</code>
<br><a href="http://snipplr.com/view.php?codeview&amp;id=45928" rel="nofollow" target="_blank">Fuente</a>
<br>
<br>
<br><strong>
<br><span style="font-size:18pt; line-height:18pt">Acortando URL's usando bit.ly</span>
<br></strong>
<br>
<br>Esta es una util funcion en php que te ayudara a acortar URL's con la ayuda del API de bit.ly , con tu apikey y tu nombre de usuario simplemente tendras acceso a este servicio
<br>
<br><code><span style="color:#000000">

<br><span style="color:#0000BB">&lt;?
<br></span><span style="color:#007700">function&nbsp;</span><span style="color:#0000BB">bitly</span><span style="color:#007700">(</span><span style="color:#0000BB">$url</span><span style="color:#007700">)&nbsp;{
<br>&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">$content&nbsp;</span><span style="color:#007700">=&nbsp;</span><span style="color:#0000BB">file_get_contents</span><span style="color:#007700">(</span><span style="color:#DD0000">"http://api.bit.ly/v3/shorten?login=TUUSER&amp;apiKey=TUAPIKEY&amp;longUrl="</span><span style="color:#007700">.</span><span style="color:#0000BB">$url</span><span style="color:#007700">.</span><span style="color:#DD0000">"&amp;format=xml"</span><span style="color:#007700">);
<br>&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">$element&nbsp;</span><span style="color:#007700">=&nbsp;new&nbsp;</span><span style="color:#0000BB">SimpleXmlElement</span><span style="color:#007700">(</span><span style="color:#0000BB">$content</span><span style="color:#007700">);
<br>&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0000BB">$bitly&nbsp;</span><span style="color:#007700">=&nbsp;</span><span style="color:#0000BB">$element</span><span style="color:#007700">-&gt;</span><span style="color:#0000BB">data</span><span style="color:#007700">-&gt;</span><span style="color:#0000BB">url</span><span style="color:#007700">;
<br>&nbsp;&nbsp;&nbsp;&nbsp;if(</span><span style="color:#0000BB">$bitly</span><span style="color:#007700">){
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return&nbsp;</span><span style="color:#0000BB">$bitly</span><span style="color:#007700">;
<br>&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;else&nbsp;{
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return&nbsp;</span><span style="color:#DD0000">'0'</span><span style="color:#007700">;
<br>&nbsp;&nbsp;&nbsp;&nbsp;}
<br>}
<br></span><span style="color:#0000BB">?&gt;
<br></span>
</span>
</code>
<br>
<br>Forma de Uso:
<br>
<br><code><span style="color:#000000">
<span style="color:#0000BB">&lt;?&nbsp;</span><span style="color:#007700">echo&nbsp;</span><span style="color:#0000BB">bitly</span><span style="color:#007700">(</span><span style="color:#DD0000">"http://www.taringa.net"</span><span style="color:#007700">);&nbsp;</span><span style="color:#0000BB">?&gt;</span>
</span>
</code>
<br>
<br><a href="http://woorkup.com/2010/06/06/3-practical-wordpress-code-snippets-you-probably-must-know/" rel="nofollow" target="_blank">Fuente</a></div>
