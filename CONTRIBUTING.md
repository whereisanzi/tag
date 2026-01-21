# Contribuindo para TAG

Obrigado por considerar contribuir com TAG! Este documento fornece diretrizes para contribuições.

## Como Contribuir

1. **Fork o Repositório**
   ```bash
   git clone https://github.com/whereisanzi/tag.git
   cd tag
   ```

2. **Crie uma Branch**
   ```bash
   git checkout -b feature/minha-contribuicao
   ```

3. **Faça suas Alterações**
   - Siga os princípios TAG rigorosamente
   - Mantenha consistência entre Python e TypeScript
   - Adicione testes para novos exemplos
   - Use type hints/annotations

4. **Commit suas Mudanças**
   ```bash
   git commit -m "Add: descrição da contribuição"
   ```

5. **Push para sua Branch**
   ```bash
   git push origin feature/minha-contribuicao
   ```

6. **Abra um Pull Request**
   - Descreva claramente o que foi alterado
   - Referencie issues relacionadas
   - Aguarde review

## Áreas de Contribuição

- 📖 Exemplos práticos em Python e TypeScript
- 🧪 Patterns de teste avançados
- 📝 Melhorias na documentação
- 🌍 Traduções
- 💡 Templates e scaffolding tools
- 🎓 Tutoriais e guias

## Guidelines de Código

### Python
- Use Python 3.11+
- Siga PEP 8
- Use type hints
- Código funcional e imutável
- Docstrings em funções públicas

### TypeScript
- Use TypeScript 5.0+
- Siga padrões ESLint
- Use tipos explícitos
- Código funcional e imutável
- JSDoc em funções públicas

## Princípios TAG

Todas as contribuições devem seguir os 8 princípios fundamentais:

1. **Flows são Pipelines** - Composição funcional
2. **Handlers sem Lógica** - Apenas conectam transporte ↔ Flows
3. **Drivers fazem Conversões** - Traduzem formatos externos
4. **Logics são Puras** - Nunca fazem IO
5. **Adapters Transformam Estruturas** - Conversões entre camadas
6. **Gateways fazem IO** - Retornam dados brutos
7. **Protocols Definem Contratos** - Abstrações permitem trocar implementações
8. **IO nas Bordas** - Efeitos colaterais isolados

## Processo de Review

1. Mantenedor revisa o PR
2. Discussão e ajustes se necessário
3. Aprovação e merge
4. Atualização do CHANGELOG

## Código de Conduta

Este projeto segue o [Código de Conduta](CODE_OF_CONDUCT.md). Ao participar, você concorda em respeitar estes termos.

## Dúvidas?

Abra uma [issue](https://github.com/whereisanzi/tag/issues) para discussão.

---

**Obrigado por contribuir com TAG!** 🚀
