
    <template>
        <center>
            <v-app>
                <v-main>
                    <v-container>
                        <v-row>
                            <v-col>
                                <h1 class="text-uppercase">Busque endereco pelo CEP</h1>
                            </v-col>
                        </v-row>

                        <table>
                            <tr>
                                <td>
                                    Digite o CEP
                                </td>
                                <td>
                                    <MaskInput type="text" v-model="mask_cep" mask="#####-###" />
                                </td>
                            </tr>
                            <tr>
                                <td>
                                    <button @click="buscarEndereco">Consultar</button>
                                </td>
                            </tr>
                        </table>
                        <br />
                        <br />
                        <br />


                        <v-row v-if="endereco.logradouro !== ''">
                            <v-col>
                                <v-card>

                                    <v-card-text>

                                     
                                        <table>

                                            <tr>
                                                <td>Dados do CEP</td>
                                            </tr>

                                            <tr>
                                                <td>CEP</td>
                                                <td>{{ endereco.cep }}</td>
                                                <td>Logradouro</td>
                                                <td>{{ endereco.logradouro }}</td>
                                            </tr>
                                            <tr>
                                                <td>Complemento</td>
                                                <td>{{ endereco.complemento }}</td>
                                                <td>Unidade</td>
                                                <td></td>
                                            </tr>
                                            <tr>
                                                <td>Bairro</td>
                                                <td>{{ endereco.bairro }}</td>
                                                <td>Localidade</td>
                                                <td></td>
                                            </tr>
                                            <tr>
                                                <td>Cidade</td>
                                                <td>{{ endereco.cidade }}</td>
                                                <td>Estado</td>
                                                <td>{{ endereco.estado }}</td>
                                            </tr>
                                            <tr>
                                                <td>Regiao</td>
                                                <td>{{ endereco.regiao }}</td>
                                                <td>IBGE</td>
                                                <td>{{ endereco.ibge }}</td>
                                            </tr>
                                            <tr>
                                                <td>Gia</td>
                                                <td>{{ endereco.gia }}</td>
                                                <td>DDD</td>
                                                <td>{{ endereco.ddd }}</td>
                                            </tr>
                                            <tr>
                                                <td>Siafi</td>
                                                <td>{{ endereco.siafi }}</td>
                                            </tr>

                                        </table>
                                    </v-card-text>
                                </v-card>
                            </v-col>
                        </v-row>
                    </v-container>
                </v-main>
            </v-app>
        </center>
    </template>

    


   
    




<script>
    
    

    export default {
  name: "App",
  data: () => ({
    //
    cep: "",
    endereco: {
      logradouro: "",
      complemente: "",
      unidade: "",
      bairro: "",
      cidade: "",
      uf: "",
      estado:"",
      regiao:"",
      ibge:"",
      gia:"",
      ddd:"",
      siafi:"",
    },
  }),
  methods: {
    buscarEndereco() {

        if (!this.mask_cep ) {
        alert("Digite um CEP");
        return;
       }
        fetch(`https://viacep.com.br/ws/${this.mask_cep}/json/`)
          .then((response) => {
            if (response.erro) {
                throw new Error("Erro ao buscar o endereço");

  
            }
            return response.json();
            
          })
          .then((data) => {
            this.endereco.cep = data.cep;
            this.endereco.logradouro = data.logradouro;
            this.endereco.complemento = data.complemento;
            this.endereco.unidade = data.unidade;
            this.endereco.bairro = data.bairro;
            this.endereco.cidade = data.localidade;
            this.endereco.uf = data.uf;
            this.endereco.estado = data.estado;
            this.endereco.regiao = data.regiao;
            this.endereco.ibge = data.ibge;
            this.endereco.gia = data.gia;
            this.endereco.ddd = data.ddd;
            this.endereco.siafi = data.siafi;
          })
          .catch((error) => {
            console.error("Erro:", error);
           
          });
      
    },
  },
};


</script>



<style>
    body {
        background-color: powderblue;
    }
    template {
        background-color: powderblue;
    }


    table,tr, td {
        border: 3px solid black;
        border-collapse: collapse; /* CSS2 */
        background: #FFFFF0;
      
    }

    MaskInput{
        border: 0px;
    }

</style>