<template>
  <v-app id="inspire">
    <v-app-bar app color="#0E335F" text dark flat>
      <v-container class="py-0 fill-height">
        <v-avatar>
          <img
            src="https://somos.lojaiplace.com.br/wp-content/uploads/2014/03/ibookslogo.png"
            alt="John"
          />
        </v-avatar>

        <v-btn text>BookStore</v-btn>
        <v-btn text>|</v-btn>
        <v-btn text :to="{name: 'Home'}">Livros</v-btn>
        <v-btn text :to="{name: 'Autor'}">Autores</v-btn>

        <v-spacer></v-spacer>

        <v-responsive max-width="260">
          <v-text-field
            placeholder="Pesquise o seu livro.."
            dense
            flat
            hide-details
            rounded
            solo-inverted
          ></v-text-field>
        </v-responsive>
      </v-container>
    </v-app-bar>

    <v-main class="grey lighten-3">
      <v-container>
        <v-row>
          <v-col cols="3">
            <v-sheet rounded="lg">
              <!-- <v-list color="transparent">
                <v-list-item>
                  <v-list-item-content>
                    <v-list-item-title>
                      <v-btn color="error" depressed block>Livros</v-btn>
                    </v-list-item-title>
                  </v-list-item-content>
                </v-list-item>
                <v-list-item>
                  <v-list-item-content>
                    <v-list-item-title>Autores</v-list-item-title>
                  </v-list-item-content>
                </v-list-item>

                <v-divider class="my-2"></v-divider>

                <v-list-item link color="grey lighten-4">
                  <v-list-item-content>
                    <v-list-item-title>Refresh</v-list-item-title>
                  </v-list-item-content>
                </v-list-item>
              </v-list>-->
              <v-card class="mx-auto" color="error" dark max-width="400">
                <!-- <v-card-title>
                  <v-icon large left>mdi-twitter</v-icon>
                  <span class="text-h6 font-weight-light">Twitter</span>
                </v-card-title> -->

                <v-card-text class="text-h5 font-weight-bold">
                  “A gente pensa uma coisa, acaba escrevendo outra e o leitor entende uma terceira coisa.
                  E enquanto se passa tudo isso, a coisa propriamente dita começa a desconfiar que não foi propriamente dita”.
                </v-card-text>

                <v-card-actions>
                  <v-list-item class="grow">
                    <v-list-item-avatar color="grey darken-3">
                      <v-img
                        class="elevation-6"
                        alt
                        src="https://avataaars.io/?avatarStyle=Transparent&topType=ShortHairShortCurly&accessoriesType=Prescription02&hairColor=Black&facialHairType=Blank&clotheType=Hoodie&clotheColor=White&eyeType=Default&eyebrowType=DefaultNatural&mouthType=Default&skinColor=Light"
                      ></v-img>
                    </v-list-item-avatar>

                    <v-list-item-content>
                      <v-list-item-title>Mário Quintana</v-list-item-title>
                    </v-list-item-content>
                  </v-list-item>
                </v-card-actions>
              </v-card>
            </v-sheet>
          </v-col>

          <v-col cols="9">
            <v-row>
              <v-col cols="9"></v-col>
              <v-col cols="3">
                <template>
                  <v-row justify="center" class="pa-4">
                    <v-dialog v-model="dialog" persistent max-width="600px">
                      <template v-slot:activator="{ on, attrs }">
                        <v-btn color="error" block dark v-bind="attrs" v-on="on">
                          <v-icon class="mr-1">mdi-plus-circle</v-icon>Livro
                        </v-btn>
                      </template>
                      <v-card>
                        <v-toolbar color="#0E335F" dark>Adicionar Livro</v-toolbar>
                        <!-- <v-card-title>
                          <span class="text-h5">User Profile</span>
                        </v-card-title>-->
                        <v-card-text>
                          <v-container>
                            <v-row>
                              <v-col cols="12" sm="6" md="6">
                                <v-text-field label="Nome"></v-text-field>
                              </v-col>
                              <v-col cols="12" sm="6" md="6">
                                <v-text-field label="Paginas" persistent-hint required></v-text-field>
                              </v-col>
                              <v-col cols="12" sm="6" md="6">
                                <v-text-field label="Preco" required></v-text-field>
                              </v-col>

                              <v-col cols="12" sm="6" md="6">
                                <v-select
                                  :items="['0-17', '18-29', '30-54', '54+']"
                                  label="Autor"
                                  required
                                ></v-select>
                              </v-col>
                            </v-row>
                          </v-container>
                        </v-card-text>
                        <v-card-actions>
                          <v-spacer></v-spacer>
                          <v-btn color="error" dark @click="dialog = false">Cancelar</v-btn>
                          <v-btn color="#0E335F" dark @click="dialog = false">Salvar</v-btn>
                        </v-card-actions>
                      </v-card>
                    </v-dialog>
                  </v-row>
                </template>
              </v-col>
            </v-row>
            <hr />
            <v-sheet min-height="70vh" rounded="lg">
              <h2 class="pa-2">Lista de Livros</h2>
              <v-simple-table>
                <template v-slot:default>
                  <thead>
                    <tr>
                      <th class="text-left">Nome</th>
                      <th class="text-left">Paginas</th>
                      <th class="text-left">Preco</th>
                      <th class="text-left">Autor</th>
                      <th class="text-left">Accoes</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="item in livros.data" :key="item.id">
                      <td>{{ item.name }}</td>
                      <td>{{ item.pages }}</td>
                      <td>{{ item.price }} MZN</td>
                      <td>{{ item.autor.name }}</td>
                      <td>
                        <v-btn class="mx-2" fab dark small color="#FF6060">
                          <v-icon dark>mdi-pencil-outline</v-icon>
                        </v-btn>
                        <v-btn class="mx-2" fab dark small color="#0E335F">
                          <v-icon dark>mdi-delete-restore</v-icon>
                        </v-btn>
                      </td>
                    </tr>
                  </tbody>
                </template>
              </v-simple-table>
            </v-sheet>
          </v-col>
        </v-row>
      </v-container>

      <v-footer padless>
        <v-col class="text-center" cols="12">
          {{ new Date().getFullYear() }} —
          <strong>Designed by Marino Ricardo</strong>
        </v-col>
      </v-footer>
    </v-main>
  </v-app>
</template>

<script>
import axios from 'axios'
/* eslint-disable */
export default {
  data: () => ({
    dialog: false,
    livros: [],
    links: [
      'Livros',
      'Autores',
    ],
    desserts: [
      {
        name: 'Frozen Yogurt',
        calories: 159,
      },
    ]
  }),

  created() {
    axios.get('http://127.0.0.1:8000/api/livros').then((data) => {
      this.livros = data.data
      console.log(data)
    })
  }
}
</script>