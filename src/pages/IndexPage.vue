<template>
  <div class="q-pa-md" style="max-width: 400px">

    <q-form
      @submit="onSubmit"
      @reset="onReset"
      class="q-gutter-md"
    >


    <!-- ID -->
      <q-input
        filled
        v-model="id"
        label="ใส่รหัสนักศึกษา *"
        hint="รหัสนักศึกษา"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'กรุณาใส่รหัสนักศึกษา']"
      />

    <!-- NAME -->
      <q-input
        filled
        v-model="name"
        label="ใส่ชื่อ *"
        hint="ชื่อจริง"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'กรุณาใส่ชื่อ']"
      />

      <!-- Surname -->
      <q-input
        filled
        v-model="surname"
        label="ใส่นามสกุล *"
        hint="นามสกุล"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'กรุณาใส่นามสกุล']"
      />

      <!-- LANGUAGE -->
      <q-input
        filled
        v-model="language"
        label="ภาษา *"
        hint="ภาษา"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'กรุณาใส่ภาษา']"
      />


      <!-- AGE -->
      <q-input
        filled
        type="number"
        v-model="age"
        label="ใส่อายุ *"
        lazy-rules
        :rules="[
          val => val !== null && val !== '' || 'กรุณาใส่อายุของคุณ',
          val => val > 0 && val < 100 || 'กรุณาใส่อายุตามความจริง'
        ]"
      />

      <q-toggle v-model="accept" label="ยอมรับเงื่อนไข" />

      <div>
        <q-btn label="Submit" type="submit" color="primary"/>
        <q-btn label="Reset" type="reset" color="primary" flat class="q-ml-sm" />
      </div>
    </q-form>

  </div>
</template>

<script>
import { useQuasar } from 'quasar'
import { ref } from 'vue'

export default {
  setup () {
    const $q = useQuasar()

    const id = ref('6604101361')
    const name = ref('พีระพัฒน์')
    const surname = ref('มิคะนุช')
    const language = ref(null)
    const age = ref(null)
    const accept = ref(false)

    return {

      id,
      name,
      surname,
      language,
      age,
      accept,

      onSubmit () {
        if (accept.value !== true) {
          $q.notify({
            color: 'red-5',
            textColor: 'white',
            icon: 'warning',
            message: 'You need to accept the license and terms first'
          })
        }
        else {
          $q.notify({
            color: 'green-4',
            textColor: 'white',
            icon: 'cloud_done',
            message: 'Submitted'
          })
        }
      },

           //reset
      onReset () {

        id.value = null
        name.value = null
        surname.value = null
        age.value = null
        accept.value = false

      }
    }
  }
}
</script>
