<template>
  <main>
    <article>
      <h1>My Article</h1>

      <section v-for="(header, index) in headers" :key="header">
        <h2 :id="index">{{ header }}</h2>
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Ipsam nesciunt nihil consectetur aperiam repellat
          doloremque dolorum veniam excepturi nemo perferendis quaerat magnam, saepe quo exercitationem quis atque nostrum
          quidem facilis. Quo ducimus reprehenderit aperiam blanditiis numquam. Eveniet, velit! Quod maxime ratione, quia
          optio, deleniti cum, laboriosam dignissimos explicabo hic illo provident! Rerum quam non et ut, quas neque.
          Facere laboriosam sint at reprehenderit quam facilis dolore enim eligendi corporis nesciunt fuga dolorem
          suscipit, repudiandae aut odio accusamus. Cum libero recusandae dolore perspiciatis sed provident doloremque
          dicta est. Ab dignissimos distinctio nemo veniam, vero unde commodi nobis, libero harum voluptatum itaque sit.
          Autem aliquid modi amet voluptatibus iste deleniti. Rerum et unde enim corrupti quos exercitationem consectetur,
          eius magnam quidem ipsum! Quia quaerat facilis dicta modi harum tempora deserunt assumenda fugit repudiandae ad
          consequuntur, perferendis earum sint tenetur atque aliquid eaque consequatur repellendus alias illum magnam
          dignissimos hic nesciunt debitis? Ut, a repudiandae earum iure labore suscipit corrupti, laborum sequi id optio
          et odio facilis itaque quod! Debitis voluptates aspernatur cupiditate quisquam est ex? Ab tempora ut, a quae
          beatae, incidunt reiciendis expedita, asperiores eius error perferendis sint sapiente nam assumenda et nihil
          atque sequi recusandae dolor dolorem? Ullam, consectetur fugiat.</p>
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Ipsam nesciunt nihil consectetur aperiam repellat
          doloremque dolorum veniam excepturi nemo perferendis quaerat magnam, saepe quo exercitationem quis atque nostrum
          quidem facilis. Quo ducimus reprehenderit aperiam blanditiis numquam. Eveniet, velit! Quod maxime ratione, quia
          optio, deleniti cum, laboriosam dignissimos explicabo hic illo provident! Rerum quam non et ut, quas neque.
          Facere laboriosam sint at reprehenderit quam facilis dolore enim eligendi corporis nesciunt fuga dolorem
          suscipit, repudiandae aut odio accusamus. Cum libero recusandae dolore perspiciatis sed provident doloremque
          dicta est. Ab dignissimos distinctio nemo veniam, vero unde commodi nobis, libero harum voluptatum itaque sit.
          Autem aliquid modi amet voluptatibus iste deleniti. Rerum et unde enim corrupti quos exercitationem consectetur,
          eius magnam quidem ipsum! Quia quaerat facilis dicta modi harum tempora deserunt assumenda fugit repudiandae ad
          consequuntur, perferendis earum sint tenetur atque aliquid eaque consequatur repellendus alias illum magnam
          dignissimos hic nesciunt debitis? Ut, a repudiandae earum iure labore suscipit corrupti, laborum sequi id optio
          et odio facilis itaque quod! Debitis voluptates aspernatur cupiditate quisquam est ex? Ab tempora ut, a quae
          beatae, incidunt reiciendis expedita, asperiores eius error perferendis sint sapiente nam assumenda et nihil
          atque sequi recusandae dolor dolorem? Ullam, consectetur fugiat.</p>
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Ipsam nesciunt nihil consectetur aperiam repellat
          doloremque dolorum veniam excepturi nemo perferendis quaerat magnam, saepe quo exercitationem quis atque nostrum
          quidem facilis. Quo ducimus reprehenderit aperiam blanditiis numquam. Eveniet, velit! Quod maxime ratione, quia
          optio, deleniti cum, laboriosam dignissimos explicabo hic illo provident! Rerum quam non et ut, quas neque.
          Facere laboriosam sint at reprehenderit quam facilis dolore enim eligendi corporis nesciunt fuga dolorem
          suscipit, repudiandae aut odio accusamus. Cum libero recusandae dolore perspiciatis sed provident doloremque
          dicta est. Ab dignissimos distinctio nemo veniam, vero unde commodi nobis, libero harum voluptatum itaque sit.
          Autem aliquid modi amet voluptatibus iste deleniti. Rerum et unde enim corrupti quos exercitationem consectetur,
          eius magnam quidem ipsum! Quia quaerat facilis dicta modi harum tempora deserunt assumenda fugit repudiandae ad
          consequuntur, perferendis earum sint tenetur atque aliquid eaque consequatur repellendus alias illum magnam
          dignissimos hic nesciunt debitis? Ut, a repudiandae earum iure labore suscipit corrupti, laborum sequi id optio
          et odio facilis itaque quod! Debitis voluptates aspernatur cupiditate quisquam est ex? Ab tempora ut, a quae
          beatae, incidunt reiciendis expedita, asperiores eius error perferendis sint sapiente nam assumenda et nihil
          atque sequi recusandae dolor dolorem? Ullam, consectetur fugiat.</p>
      </section>
    </article>

    <aside>
      <div>
        {{ currentSection }}
        <!-- <a v-for="(header, index) in headers" :key="header" :href="`#${index}`"
          :class="{ active: index == currentSection }">
          {{ header }}
        </a> -->

        <a v-for="(header, index) in headers" :key="header" @click="scrollMeTo(index)"
          :class="{ active: index == currentSection }">
          {{ header }}
        </a>
      </div>
    </aside>
  </main>
</template>

<script setup>
// https://www.youtube.com/watch?v=dozWGIgCWF8&t=217s
import { ref, onMounted } from 'vue';

function scrollMeTo(refName) {
  const element = document.getElementById(refName);
  window.scrollTo(0, (element.offsetTop - 50))

}

const headers = [
  'Section 1',
  'Section 2',
  'How This Works',
  'Placeholder',
  'Section 5'
];

const currentSection = ref('');

onMounted(() => {

  const observer = new IntersectionObserver(
    entries => {
      entries.forEach(entry => {
        console.log(entry)
        // intersectionRatio tells how much of the target element is currently visible in our bounds 
        if (entry.intersectionRatio > 0) {
          currentSection.value = entry.target.getAttribute('id');
        }
      });
    },
    {
      rootMargin: '0px 0px -90% 0px'
    }
  );

  document.querySelectorAll('article h2').forEach(section => {
    observer.observe(section);
  });

});

</script>

<style>
* {
  box-sizing: border-box;
}

html,
body {
  color: #2c3e50;
}

p {
  line-height: 1.5;
}

h2 {
  margin-bottom: 2px;
}

main {
  display: flex;
  max-width: 1080px;
  margin: auto;
}

article {
  /* margin-bottom: 500px; */
}

aside {
  width: 25%;
}

aside>div {
  position: sticky;
  top: 20px;
  padding-left: 2em;
}

aside>div>a {
  display: block;
  color: #2c3e50;
  text-decoration: none;
  border-left: 1px solid rgba(180, 29, 222, 0.2);
  padding-left: 2em;
  white-space: nowrap;
  padding: 8px;
}

aside a.active {
  font-weight: bold;
  border-width: 3px;
  margin-left: -2px;
  border-color: #b41dde;
}
</style>
