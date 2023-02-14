<script setup>
  // components
  import PageTitle from './components/PageTitle.vue'
  import Notification from './components/Notification.vue'

  //
  import { ref } from 'vue'

  const formAction = ref('https://FormAction.com')
  const fields = ref([{ name: 'hotel', value: 'trivago' }])

  /**
   *
   */
  const addItem = () => {
    fields.value.push({ name: '', value: '' })
  }

  /**
   *
   */
  const removeLastItem = () => {
    fields.value.pop()
  }

  /**
   *
   */
  const submitForm = () => {
    // eval if form already exists, if it does, remove it
    let formToSubmit = document.getElementById('formMain')

    if (!!document.getElementById('formMain')) {
      formToSubmit.remove()
      console.info('Removed duplicate form.')
    }

    // create form
    const submitForm = document.createElement('form')
    submitForm.setAttribute('method', 'POST')
    submitForm.setAttribute('action', formAction.value)
    submitForm.setAttribute('target', '_blank')
    submitForm.setAttribute('id', 'formMain')

    // create and add each data to the form
    fields.value.forEach((field) => {
      // console.log(`${field.name}: ${field.value}`)

      const textInput = document.createElement('input')
      textInput.setAttribute('type', 'hidden')
      textInput.setAttribute('name', field.name)
      textInput.setAttribute('value', field.value)
      submitForm.appendChild(textInput)
    })

    document.body.appendChild(submitForm)

    submitForm.submit()
  }
</script>

<template>
  <div class="container m-auto px-40">
    <div class="my-12">
      <PageTitle>Post Baby</PageTitle>
      <p>This bad boi will submit your data.</p>
    </div>

    <Notification title="Instructions">
      Put the <span class="nes-text is-warning">POST URL</span> in the Form
      Action input below and then add as many data fields as you like!
    </Notification>

    <!-- main content -->
    <div>
      <!-- FORM ACTION INPUT -->
      <div class="nes-field my-6">
        <label for="name_field">Form Action (POST)</label>
        <input
          type="text"
          class="nes-input"
          spellcheck="false"
          v-model="formAction" />
      </div>

      <!-- FIELDS -->
      <div class="flex flex-col gap-6">
        <!-- LOOP HERE -->
        <TransitionGroup class="flex flex-col gap-6" name="list" tag="div">
          <div class="flex gap-3" v-for="field in fields">
            <div class="flex-auto w-96">
              <div class="nes-field">
                <label for="name_field">Name</label>
                <input
                  type="text"
                  class="nes-input"
                  spellcheck="false"
                  v-model="field.name" />
              </div>
            </div>

            <div class="flex-auto w-full">
              <div class="nes-field">
                <label for="name_field">Value</label>
                <input
                  type="text"
                  class="nes-input"
                  spellcheck="false"
                  v-model="field.value" />
              </div>
            </div>
          </div>
        </TransitionGroup>
        <!-- BUTTONS!!! -->
        <div class="flex">
          <div class="flex-1">
            <div class="flex gap-3">
              <button class="nes-btn is-primary" @click="addItem">
                Add New
              </button>

              <button class="nes-btn is-error" @click="removeLastItem">
                Remove
              </button>
            </div>
          </div>

          <div class="flex flex-row-reverse">
            <button class="nes-btn is-success" @click="submitForm">
              Submit
            </button>
          </div>
        </div>
      </div>
    </div>

    <!-- FOOTER -->
    <footer class="my-24 text-center">
      <a href="https://github.com/veib6247/post-baby" target="_blank">Github</a>
    </footer>
  </div>
</template>

<style scoped>
  /** for fields transition */
  .list-enter-active,
  .list-leave-active {
    transition: all 0.5s ease;
  }
  .list-enter-from,
  .list-leave-to {
    opacity: 0;
    transform: translateX(30px);
  }
</style>
