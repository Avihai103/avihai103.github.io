<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css">
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.16.0/umd/popper.min.js"></script>
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js"></script>
    <title>Game</title>
</head>
<style>
    body{
        margin: 60px;
    }
    .rectangle{
        border: 1px solid gray;
        padding: 5px;
    }
    .A-offer, .B-offer, .AB-offer{
        height: 150px;
    }
    .screen2, .screen3, .screen4, .gameEnd{
        display: none;
    }
    .loaderr{
        position: fixed;
        left: 0px;
        top: 0px;
        width: 100%;
        height: 100%;
        z-index: 9999;
    }

</style>
<body>
    <div class="container">

        <div class="screen1">

            <h4>Dear Intel's representative, please select which of the companies you would like to approch:</h4>
            <hr>
            <br><br>
           <div class="row">
               <div class="col-md-2 text-center company" id="A">
                <div class="rectangle">Apple</div>
               </div>
               <div class="col-md-2 text-center company" id="B">
                <div class="rectangle">IBM</div>
               </div>
               <div class="col-md-2 text-center company" id="AB">
                <div class="rectangle">Apple & IBM</div>
               </div>
           </div>

        </div>

        <div class="screen2">

           <div class="row">
               <div class="col-md-4 A-offer">
                    <div class="rectangle">Offer you division of the 84 million dollars between you and Apple:
                        <div class="row" style="margin-top:12px;">
                            <div class="form-group col-md-6">
                                <label for="AYou">You:</label>
                                <input type="number" class="form-control" placeholder="value in million" id="AYou" min="0" max="84">
                            </div>
                            <div class="form-group col-md-6">
                                <label for="AFilled">Apple:</label>
                                <input type="number" class="form-control" placeholder="" id="AFilled">
                            </div>
                            <div class="col-md-12">
                                <button class="sent" disabled>sent</button>
                            </div>
                        </div>
                    </div>
               </div>
               <div class="col-md-4 B-offer">
                    <div class="rectangle">Offer you division of the 40 million dollars between you and IBM:
                        <div class="row" style="margin-top:12px;">
                            <div class="form-group col-md-6">
                                <label for="BYou">You:</label>
                                <input type="number" class="form-control" placeholder="value in million" id="BYou" min="0" max="40">
                            </div>
                            <div class="form-group col-md-6">
                                <label for="BFilled">IBM:</label>
                                <input type="number" class="form-control" placeholder="" id="BFilled">
                            </div>
                            <div class="col-md-12">
                                <button class="sent" disabled>sent</button>
                            </div>
                        </div>
                    </div>
               </div>
               <div class="col-md-6 AB-offer">
                <div class="rectangle">Offer you division of the 121 million dollars between you,Apple and IBM:
                    <div class="row" style="margin-top:12px;">
                        <div class="form-group col-md-4">
                            <label for="ABYou">You:</label>
                            <input type="number" class="form-control" placeholder="value in million" id="ABYou" min="0" max="121">
                        </div>
                        <div class="form-group col-md-4">
                            <label for="ABA">Apple:</label>
                            <input type="number" class="form-control" placeholder="value in million" id="ABA" min="0" max="121">
                        </div>
                        <div class="form-group col-md-4">
                            <label for="ABFilled">IBM:</label>
                            <input type="number" class="form-control" placeholder="" id="ABFilled">
                        </div>
                        <div class="col-md-12">
                            <button class="sent" disabled>sent</button>
                        </div>
                    </div>
                </div>
               </div>
           </div>

        </div>

        <div class="screen3">
            <img src="loader.gif" alt="" class="loader">
        </div>

        <div class="screen4">
            <h4></h4>
            <!-- <h4>A and B are planning to reach an agreement between themselves with a devision of (<span id="firstPlace"></span>, <span id="secondPlace"></span>).</h4> -->
            <p id="loop">
                Would you like to suggest a new division?
                <button id="yes">Yes</button>
                <button id="no">No</button>
            </p>
        </div>

        <div class="gameEnd">
            <h4>Game over - IBM and Apple reached an agreement and Intel earned 0.</h4>
        </div>

    </div>


    <script>

        $( document ).ready(function() {
            var companyId = '';
            $('.company').click(function(){
                companyId = $(this).attr('id');
                $('.screen1').hide();
                $('.screen2').show();
                if(companyId == 'A'){
                    $('.A-offer').show();
                    $('.B-offer').hide();
                    $('.AB-offer').hide();
                }
                if(companyId == 'B'){
                    $('.A-offer').hide();
                    $('.B-offer').show();
                    $('.AB-offer').hide();
                }
                if(companyId == 'AB'){
                    $('.A-offer').hide();
                    $('.B-offer').hide();
                    $('.AB-offer').show();
                }

            })


            $("#AYou").bind('keyup mouseup', function () {
                if($(this).val() !== ''){
                $('#AFilled').val(84-$(this).val()); 

                if($(this).val() >= 0 || $(this).val() <= 84){
                    $('.sent').prop("disabled", false);
                }
                if($(this).val() < 0 || $(this).val() > 84){
                    $('.sent').prop("disabled", true);
                }
                        
                }
            });

            $("#BYou").bind('keyup mouseup', function () {
                if($(this).val() !== ''){
                $('#BFilled').val(40-$(this).val());  

                 if($(this).val() >= 0 || $(this).val() <= 40){
                    $('.sent').prop("disabled", false);
                }
                if($(this).val() < 0 || $(this).val() > 40){
                    $('.sent').prop("disabled", true);
                }

                }
            });

            $("#ABA, #ABYou").bind('keyup mouseup', function () {
                if($(this).val() !== ''){
                    var AB_you = parseFloat($('#ABYou').val());
                    var AB_A = parseFloat($('#ABA').val());
                    var ans = AB_you + AB_A;
                    $('#ABFilled').val(121-ans);  

                    if((AB_you >= 0 || AB_you <= 121) && (AB_A >= 0 || AB_A <= 121)){
                        $('.sent').prop("disabled", false);
                    }
                    if((AB_you < 0 || AB_you > 121) || (AB_A < 0 || AB_A > 121) ){
                        $('.sent').prop("disabled", true);
                    }

                }
            });

            

            $('.sent').click(function(){
                $('.screen2').hide();
                $('.screen3').show();

                if(companyId == 'A'){
                    setTimeout(() => {
                        var first_place = parseFloat($('#AFilled').val()) + 3;
                        var second_place = 118-( parseFloat($('#AFilled').val()) + 3 );
                        $('.screen3').hide();
                        
                        if($('#AYou').val() == 0){
                            $('.screen4 h4').text('Game over - Intel earned 0');
                            $('#loop').hide();
                        }
                        if($('#AYou').val() != 0){
                            $('.screen4 h4').text('IBM offered to Apple '+first_place+' millions dollars out of $118m,and remained with '+second_place+' million dollars for itself.');
                        }
                        $('.screen4').show();
                    }, 1000);
                }

                if (companyId == 'B') {
                    setTimeout(() => {
                        var first_place = parseFloat($('#BFilled').val()) + 3;
                        var second_place = 118-( parseFloat($('#BFilled').val()) + 3 );
                        $('.screen3').hide();
                        if($('#BYou').val() == 0){
                            $('.screen4 h4').text('Game over - Intel earned 0');
                            $('#loop').hide();
                        }
                        if($('#BYou').val() != 0){
                            $('.screen4 h4').text('Apple offered to IBM '+first_place+' millions dollars out of $118m,and remained with '+second_place+' million dollars for itself.');
                        }
                        $('.screen4').show();
                    }, 1000);
                }

                if (companyId == 'AB') {
                    setTimeout(() => {
                        var first_place = parseFloat($('#ABA').val()) + 3;
                        var second_place = 118-( parseFloat($('#ABA').val()) + 3 );
                        $('.screen3').hide();
                        if($('#ABYou').val() == 0){
                            $('.screen4 h4').text('Game over - Intel earned 0');
                            $('#loop').hide();
                        }
                        if($('#ABYou').val() > 3){
                            $('.screen4 h4').text('IBM offered to Apple '+first_place+' millions dollars out of $118m,and remained with '+second_place+' million dollars for itself.');
                        }
                        if( ($('#ABYou').val()==1||$('#ABYou').val()==2||$('#ABYou').val()==3) && ($('#ABFilled').val() < 37) ){
                            $('.screen4 h4').text('IBM doesn’t agree for this division.');
                        }
                        if( ($('#ABYou').val()==1||$('#ABYou').val()==2||$('#ABYou').val()==3) && ($('#ABA').val() < 81) ){
                            $('.screen4 h4').text('Apple doesn’t agree for this division.');
                        }
                        if( ($('#ABYou').val()==1||$('#ABYou').val()==2||$('#ABYou').val()==3) && ($('#ABA').val() >= 81) && ($('#ABFilled').val() >= 37) ){
                            $('.screen4 h4').text('Well done! you have reached an agreement with the following payoffs: you '+$('#ABYou').val()+'; Apple '+$('#ABA').val()+'; and IBM '+$('#ABFilled').val()+'.');
                            $('#loop').hide();
                        }
                        $('.screen4').show();
                    }, 1000);
                }
            })


            $('#yes').click(function(){
                $('input').val('');
                $('#loop').show();
                $('.screen4').hide();
                $('.screen1').show();
            })

            $('#no').click(function(){
                $('input').val('');
                $('.screen4').hide();
                $('.gameEnd').show();
            })

        });

    </script>
</body>
</html>
