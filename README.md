# Requete-Ajax
<p>Requete de type post,get (SuperVariable) vers l'url avec les data, on gère le success puis l'error et si on veut le beforeSend par exemple.</p>
<P>Par défaut une requête AJAX est asynchrone donc async:true on peut la passer à false et elle sera synchrone (bloque à l'étape de la requête jusqu'à qu'elle soit executé).</p>
<p>L'exemple ci-dessous représente un choix de tri et l'éxécution en JS pour effectuer la requête Ajax avec la réception de la requête Ajax et son traitement définie dans le chemin de l'url</p>

            <div class="span4">
                  <div style="margin-bottom:5px;">
                    <label><i class="fa fa-sort" aria-hidden="true"></i> Tri</label>
                      <select name="selectFiltreAgrementTri" id="selectFiltreAgrementTri" class="input-block-level">
                        <option value="recent" <?php if ( $filtreAgrementTri == 'recent' ) { echo 'selected'; } ?>>
                           Du plus récent au plus ancien
                        </option>
                        <option selected="selected" value="ancien" <?php if ( $filtreAgrementTri == 'ancien' ) { echo 'selected'; } ?>>
                           Du plus ancien au plus récent
                        </option>
                      </select>
                  </div>
           </div>
           
            $('#selectFiltreAgrementTri').on('change',function (){

            $('#fichierAgrement').html('<center><img src="img/ajax-loader.gif" style="padding:20px;"></center>');
            $.ajax({
                type: "POST",
                url: "functions/controleur.php",
                data: {
                    function: 'triAgrements',
                    ordreTri: $('#selectFiltreAgrementTri').val(),
                    ctrcode:'<?php echo $codeCtr; ?>'
                },
                success: function (result) {
                    $('#fichierAgrement').html(result);
                },
                error: function (result) {

                }
            })
        })
        
    // controleur.php réception de la requête Ajax et traitement de celle-ci pour renvoyer une info    
    if (isset($_POST["function"]) && isset($_POST["ordreTri"]) && isset($_POST["ctrcode"])){
        echo getFichiersCtr($_POST['ctrcode'],$_POST['ordreTri']);
    }
