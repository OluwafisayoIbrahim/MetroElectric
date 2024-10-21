<template>
  <div>
    <NavBar class="sticky top-0 bg-white w-full z-30" />
    <NuxtPage :data="cards" :news="news" />
    <Footer class="p-5" />
  </div>
</template>

<script lang="ts" setup>
import type { Card, NewsItem } from "~/types/types";
const cards: Card[] = [
  {
    link: "corporate-ev-fleet",
    image: "corporate.webp",
    title: "Fleet360: Corporate Electric Vehicles (EV) Fleet",
    description:
      "We offer comprehensive Electric Vehicles (EV) solutions tailored to corporate clients in Africa. Our services include supplying a diverse range of Electric Vehicles, such as Cars, Buses, tricycles, and Pickups, that facilitate employee mobility and dispatch.",
  },
  {
    link: "green-fleet",
    image: "greenfleet.webp",
    title: "GreenFleet: Public Transportation Renewal ",
    description:
      "GreenFleet is our Electric Vehicles (EV) Fleet Renewal Initiative for Public Transportation, developed in collaboration with governments at various levels. This initiative focuses on integrating Electric Vehicles (EV) into public transportation systems, including tricycles, minicars, taxis, minibuses, and buses. By transitioning to EVs, we aim to create greener, cleaner cities while enhancing the efficiency and sustainability of public transport networks.",
  },
  {
    link: "metro-charge",
    image: "metro.webp",
    title: "Metro Charge: Electric Vehicles (EV) Charging Infrastructure ",
    description:
      "Recognising the importance of supporting infrastructure, Metro Charge is our network of Electric Vehicles (EV) charging stations in partnership with Sunphos, dedicated to ensuring seamless and convenient charging for all Electric Vehicles (EV) users. Our stations will be strategically located to provide easy access and reliability, supporting the growing adoption of EVs across the continent.",
  },
  {
    link: "ryde",
    image: "ryde.webp",
    title: "RYDE: Ride-Hailing And Sharing Services ",
    description:
      "RYDE is our innovative ride-hailing, sharing, charter, and taxi service. Starting in Nigeria, RYDE will deploy a fleet of owned Electric Vehicles (EV) assets, offering affordable, convenient, safe, and eco-friendly transportation. Positioned to rival global giants like Uber, Bolt, and Lyft, RYDE aims to redefine urban mobility in Africa",
  },
  {
    link: "assembli",
    image: "assembli.webp",
    title: "ASSEMBLI: Electric Vehicles (EV) Assembly Network ",
    description:
      "ASSEMBLI is our extensive network of Electric Vehicles (EV) Assembly Plants dedicated to assembling Electric Vehicles, including tricycles, cars, and buses. This network ensures high-quality production standards, reduces costs, and expedites the delivery of EVs to various markets across Africa. By building and assembling vehicles locally, we support local economies and create job opportunities.",
  },
  {
    link: "ev-care",
    image: "evCare.webp",
    title:
      "Electric Vehicles (EV) Care: Electric Vehicles (EV) Maintenance Services ",
    description:
      "Electric Vehicles (EV) Care offers comprehensive maintenance services to ensure your EV fleet's longevity and optimal performance. Our network of specialised service and maintenance garages will be equipped with the latest technology and staffed by trained professionals. From routine maintenance to advanced repairs, we provide support to keep your Electric Vehicles running smoothly and efficiently.",
  },
];

const news: NewsItem[] = [
  {
    title: "Groundbreaking Electric Vehicle Technology Unveiled",
    description:
      "Today, a new wave of electric vehicle technology was introduced, set to revolutionize the industry.",
    content:
      "Today, a new wave of electric vehicle technology was introduced, set to revolutionize the industry. This advancement promises longer battery life, faster charging, and more affordable EV options for the public.",
    image: "pause",
    date: "2024-10-15",
    slug: "groundbreaking-ev-tech-unveiled",
  },
  {
    title: "Metropolitan Electric Launches Sustainable Energy Program",
    description:
      "In an effort to combat climate change, Metropolitan Electric announced a new sustainable energy initiative.",
    content:
      "In an effort to combat climate change, Metropolitan Electric announced a new sustainable energy initiative. This program focuses on increasing renewable energy use in homes and businesses across Nigeria.",
    image: "pause",
    date: "2024-10-10",
    slug: "sustainable-energy-program-launch",
  },
  {
    title: "New Recycling Facility Opens in Lagos",
    description:
      "A state-of-the-art recycling facility has opened in Lagos, capable of processing over 100 tons of plastic waste daily.",
    content:
      "A state-of-the-art recycling facility has opened in Lagos, capable of processing over 100 tons of plastic waste daily. This facility is a major step forward in Nigeria’s fight against pollution.",
    image: "pause",
    date: "2024-10-05",
    slug: "new-recycling-facility-lagos",
  },
  {
    title: "Electric Vehicle Sales Surge in 2024",
    description:
      "Reports show that electric vehicle sales have surged by 25% this year.",
    content:
      "Reports show that electric vehicle sales have surged by 25% this year, with more Nigerians adopting EVs as a sustainable alternative to traditional fuel-powered vehicles.",
    image: "pause",
    date: "2024-09-30",
    slug: "ev-sales-surge-2024",
  },
  {
    title: "Government Introduces New Environmental Regulations",
    description:
      "The Nigerian government has introduced new regulations aimed at reducing carbon emissions and promoting sustainable energy solutions.",
    content:
      "The Nigerian government has introduced new regulations aimed at reducing carbon emissions and promoting sustainable energy solutions. These regulations are set to take effect in January 2025.",
    image: "pause",
    date: "2024-09-20",
    slug: "new-environmental-regulations",
  },
];
</script>
<style>
html {
  font-family: "Varela Round", sans-serif;
  scroll-behavior: smooth;
  scroll-padding: 10rem;
}
</style>
