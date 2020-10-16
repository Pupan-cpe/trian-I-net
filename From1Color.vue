<template>
  <v-card
    style="width:60%; margin-left:20%;"
    color="blue lighten-5"
  >
    <br>

    <v-card
      style="width:80%;  margin-left:10%;"
    >
      <v-container>
        <v-form
          ref="form"
          v-model="valid"
          lazy-validation
        >
          <!-- /////////////////////////////////////////////////////////////////////////////////////// -->
          <v-text-field
            v-model="name"
            :rules="[value => !!value || 'จำเป็นต้องกรอกข้อมูล']"
            label="ชื่อฟาร์ม"
            required
          />
          <v-text-field
            v-model="fullname"
            :rules="[value => !!value || 'จำเป็นต้องกรอกข้อมูล']"
            label="ชื่อ-สกุล เจ้าของฟาร์ม"
            required
          />
          <v-text-field
            v-model="id"
            :counter="13"
            label="เลขบัตรประจำตัวประชาชน"
            :rules="idRules"
            required
          />
          <v-text-field
            v-model="idfarm"
            label="เลขที่ทะเบียนฟาร์ม"
            required
          />

          <v-select
            v-model="select"
            :items="items"
            :rules="[v => !!v || 'Item is required']"
            label="Item"
            required
          />

          <v-row>
            <v-col
              cols="12"
              sm="2"
              md="2"
            >
              <br>
              <v-text

                align="left"
              >
                มาตรฐานฟาร์ม
              </v-text>
            </v-col>

            <v-col
              cols="12"
              sm="2"
              md="2"
            >
              <v-checkbox
                v-model="ex4"
                label="CoC"
                color="red"
                value="red"
                :rules="checkboxRules"
                hide-details
              />
            </v-col>
            <v-col
              cols="12"
              sm="2"
              md="2"
            >
              <v-checkbox
                v-model="ex4"
                label="GAP"
                color="indigo"
                value="indigo"
                :rules="checkboxRules"
                hide-details
              />
            </v-col>
            <v-col
              cols="12"
              sm="2"
              md="2"
            >
              <v-checkbox
                v-model="ex4"
                label="New GAP"
                color="indigo"
                value="indigo"
                :rules="checkboxRules"
                hide-details
              />
            </v-col>
            <v-col
              cols="12"
              sm="2"
              md="2"
            >
              <v-checkbox
                v-model="ex4"
                label="BAP"
                color="orange"
                value="orange"
                :rules="checkboxRules"
                hide-details
              />
            </v-col>
            <v-col
              cols="6"
              sm="1"
              md="1"
            >
              <v-card-text>
                <v-row align="center">
                  <v-checkbox
                    v-model="enabled"
                    label="Other"
                    hide-details
                    class="shrink mr-2 mt-0"
                  />
                  <v-text-field
                    :disabled="!enabled"
                    label=" "
                  />
                </v-row>
              </v-card-text>
            </v-col>
          </v-row>
          <v-col
            cols="12"
            sm="6"
            md="6"
          >
            <v-text-field
              v-model="idfarm"
              label="ที่อยู่"
              required
            />
            <br>
          </v-col>
        </v-form>
      </v-container>
    </v-card>
    <v-btn
      :disabled="!valid"
      color="success"
      @click="validate"
    >
      Validate
    </v-btn>

    <v-btn
      color="error"
      @click="reset"
    >
      Reset Form
    </v-btn>

    <v-btn
      color="warning"
      @click="resetValidation"
    >
      Reset Validation
    </v-btn>
    <v-spacer style="height:10px" />
  </v-card>
</template>
<script>
  import ThailandAutoComplete from 'vue-thailand-address-autocomplete'
  export default {

    data: () => ({
      components: {
        ThailandAutoComplete,
      },
      district: '',
      amphoe: '',
      province: '',
      zipcode: '',
      fullname: '',
      idfarm: '',

      valid: true,
      enabled: false,
      id: '',
      idRules: [
        v => !!v || 'กรุณากรอกเลขบัตรประจำตัวประชาชน',
        v =>
          (!isNaN(parseInt(v)) && v >= 0 && v.length === 13) ||
          'กรุณากรอกเฉพาะตัวเลขให้ครบ13หลัก',
      ],

      name: '',
      nameRules: [
        v => !!v || 'Name is required',
        v => (v && v.length <= 10) || 'Name must be less than 10 characters',
      ],

      select: null,
      items: ['Item 1', 'Item 2', 'Item 3', 'Item 4'],
      checkbox: false,
    }),
    checkboxRules: [
      v => !!v || 'E-mail is required',
      v => (v.length > 0) || 'Name must be less than 10 characters',
    ],

    methods: {
      select (address) {
        this.district = address.district
        this.amphoe = address.amphoe
        this.province = address.province
        this.zipcode = address.zipcode
      },
      validate () {
        if (this.$refs.form.validate()) {
          this.snackbar = true
        }
      },
      reset () {
        this.$refs.form.reset()
      },
      resetValidation () {
        this.$refs.form.resetValidation()
      },
    },
  }
</script>
