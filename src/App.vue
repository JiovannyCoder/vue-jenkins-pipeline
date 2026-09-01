<script setup lang="ts">
import {
  Field,
  FieldDescription,
  FieldGroup,
  FieldLabel,
  FieldSet,
} from '@/components/ui/field'
import { Input } from '@/components/ui/input'
import {
  Card,
  CardContent,
  CardDescription,
  CardHeader,
  CardTitle,
} from '@/components/ui/card'
import { Textarea } from '@/components/ui/textarea';
import Button from './components/ui/button/Button.vue';
import { ref } from 'vue';
import { toast } from 'vue-sonner';
import { Toaster } from '@/components/ui/sonner'

import 'vue-sonner/style.css'

const rightAnswers = {
  name: "Escanor",
  sentence: "Who decide that ?"
}
const name = ref("")
const sentence = ref("")

const handleSubmit = () => {
  if (!name.value) {
    toast.error("The charactere name is required bro !")
    return
  }

  if (!sentence.value) {
    toast.error("The sentence is required, try to guess !")
    return
  }


  if (name.value == rightAnswers.name) {
    toast.success(`Yes my friend, it's ${rightAnswers.name} !`)
  }

  if (sentence.value == rightAnswers.sentence) {
    toast.success(`You're a legend, that's what ${rightAnswers.name} said bro !`)
  }
}
</script>

<template>
  <main>
    <form @submit.prevent="handleSubmit">
      <Card class="w-full mx-auto max-w-md mt-[20dvh]">
        <CardHeader>
          <CardTitle>Welcome to Vue Pipeline App Success bro ! yessss</CardTitle>
          <CardDescription>
            Try to guess my anime character and favorite sentence
          </CardDescription>
        </CardHeader>
        <CardContent>
          <FieldSet>
            <FieldGroup>
              <Field>
                <FieldLabel for="name">
                  Character name
                </FieldLabel>
                <Input v-model="name" id="name" type="text" placeholder="My fav. anime antagonist" />
                <FieldDescription>
                  Try to guess my favorite anime character
                </FieldDescription>
              </Field>
              <Field>
                <FieldLabel for="sentence">
                  The legendary sentence
                </FieldLabel>
                <FieldDescription>
                  A ledendary sentence knowned by every legend
                </FieldDescription>
                <Textarea v-model="sentence" id="sentence" type="sentence" placeholder="????" />
              </Field>
            </FieldGroup>
          </FieldSet>

          <FieldSet class="mt-4">
            <Button type="submit">Try to guess</Button>
          </FieldSet>
        </CardContent>
      </Card>
    </form>
    <Toaster />
  </main>
</template>
